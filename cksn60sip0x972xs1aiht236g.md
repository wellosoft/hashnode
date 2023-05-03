---
title: "How to Redirect a domain only using DNS records"
datePublished: Sun Aug 22 2021 12:07:03 GMT+0000 (Coordinated Universal Time)
cuid: cksn60sip0x972xs1aiht236g
slug: how-to-redirect-a-domain-only-using-dns-records
tags: microservices, opensource, saas, free, domain

---

At some point in time, You might want to move your website to a new domain address but don't want people with existing URL links to your old domain to find your content is no longer found, so then you need to set up a redirect link.

You thought this was easy, but turns out it isn't. You need a separate server for that. Who would want to purchase additional bucks just to set up a server to redirect links?

So let's meet [forwarddomain.net](https://forwarddomain.net), a simple redirect service.

All you need to do to use this service is to add a CNAME and a TXT record, like this:

```bash
www.old.com     IN    CNAME   r.forwarddomain.net
_.www.old.com   IN    TXT     forward-domain=https://old.com/*
```

This will redirect all links from `www.old.com` to `old.com`. You can also redirect to other domains, just change the `forward-domain=` part.

> Note the `_.` prefix at the TXT record!

In case you want to redirect a root or apex domain, CNAME can't be inserted there, so you can use A+AAAA records that directly bind to IP addresses of this service:

```bash
old.com     IN    A       167.172.5.31
old.com     IN    AAAA    2400:6180:0:d0::e08:a001
_.old.com   IN    TXT     forward-domain=https://new.net/*
```

That's it! This will redirect all links from `old.com` to `new.net`. Note the `*` part? it means also forwarding URL paths and GET query data.

This is all you need to be able to set up domain redirection of your old domain. No coding is required, no registration is required, completely free and anonymous. You can also see the [GitHub repo](https://github.com/willnode/forward-domain) since it's an open-source project anyway.

> EDIT 2021-09-21: This post is updated for [v2.0 changes](https://github.com/willnode/forward-domain/blob/main/CHANGES.md)  
> EDIT 2023-05-03: Added AAAA records for apex domain