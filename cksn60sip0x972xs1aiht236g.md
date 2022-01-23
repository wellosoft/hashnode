## How to Redirect a domain only using DNS records

At some point in time, You might want to move your website to a new domain address but don't want people with existing URL links to your old domain to find your content is no longer found, so then you need to set up a redirect link.

You thought this was easy, but turns out it isn't. You need a separate server for that. Who would want to purchase additional bucks just to set up a server to redirect links?

So let's meet [forwarddomain.net](https://forwarddomain.net), a simple redirect service.

All you need to do to use this service is to add CNAME and some TXT records, like this:

```conf
www.old.com     IN    CNAME   r.forwarddomain.net
_.www.old.com   IN    TXT     forward-domain=https://old.com/*
```

This will redirect all links from `www.old.com` to `old.com`. You can also redirect other domains, just change the `forward-domain=` part.

In case you want to redirect a root or apex domain, you can't do that with CNAME, so you can use an A record that directly binds to the IP address of this service:

```conf
old.com     IN    A       167.172.5.31
_.old.com   IN    TXT     forward-domain=https://new.net/*
```

That's it! this will redirect all links from `old.com` to `new.net`. Note the `*` part? it means also forward URL paths and GET query data.

This is all you need to be able to set up domain redirection of your old domain. No coding required, no registration required, completely free and anonymous. You can also see the [GitHub repo](https://github.com/willnode/forward-domain) since it's an open-source project anyway.

> EDIT 2021-09-21: This post is updated for [v2.0 changes](https://github.com/willnode/forward-domain/blob/main/CHANGES.md)
