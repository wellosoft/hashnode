## Stuck Trying to Migrate from CentOS Linux to Rocky Linux after EOL?

So CentOS Linux is [already passed their End of Life](https://blog.centos.org/2020/12/future-is-centos-stream/) and I forgot to migrate my system to [Rocky Linux](https://rockylinux.org/). What could be worse?

I run [the migration script today](https://github.com/rocky-linux/rocky-tools/tree/main/migrate2rocky) and I encountered this pellicular error:

```txt
Error: Error downloading packages:  No URLs in mirrorlist
``` 

I thought it was just a random network error, well it also failed with `dnf update`. Things go dark from here.

After a few hours of trial and error debugging the network. I successfully fixed it by changing the CentOS' YUM repo server to one of the mirror servers. What this is means is that the canonical  CentOS YUM repo server list (`mirrorlist.centos.org`) is simply no longer be usable anymore and we need to change it to one of the usable mirrors left in the world.
 
One of the mirrors that worked for me when I wrote this is `http://repo.uk.bigstepcloud.com/`. There are lots of other mirrors to choose from [listed here](https://mirror-status.centos.org/).

To change the CentOS YUM repo server used, you need to modify these files using `vim` or `nano` (your list may be more or less, you need to check which yum repos enabled in your machine using `yum repolist --enabled` :

```
/etc/yum.repos.d/CentOS-Linux-AppStream.repo
/etc/yum.repos.d/CentOS-Linux-BaseOS.repo
/etc/yum.repos.d/CentOS-Linux-Extras.repo
/etc/yum.repos.d/CentOS-Linux-PowerTools.repo
```

You need to comment out the `mirrorlist` and uncomment the `baseurl` with changing the mirror base URL. The changes are done like this:
```patch
[baseos]
name=CentOS Linux $releasever - BaseOS
- mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=BaseOS&infra=$infra
+ #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=BaseOS&infra=$infra
- #baseurl=http://mirrorlist.centos.org/$contentdir/$releasever/BaseOS/$basearch/os/
+ baseurl=http://repo.uk.bigstepcloud.com/$contentdir/$releasever/BaseOS/$basearch/os/
gpgcheck=1
enabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-centosofficial
```

I run the migration system again and things work so well. guess I need to share this small tip so I can save someone else's hours haha. Hope it is useful!