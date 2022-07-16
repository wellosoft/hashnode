## Switching from Google Analytics to a cookie-less solution

Web-traffic Analytics is an important metric for any web service. For me, it can be useful to see whether a project is deemed worth continuing or indeed useful for people. 

The most obvious solution is to use Google Analytics. It's robust and free. For many years people (and I) don't have a problem with it. But, recent development in data protection and privacy enforcement like GDRP makes me think a lot: Why would I have to make that annoying cookie consent just to make Google Analytics work?

For a long time, I just pulled my websites from Google Analytics. But after a while, without it, I'm clueless. I don't know if my marketing strategy would make any difference. So I search for a "cookie-less" solution so I don't need to put cookie consent. Turns out, there are a lot of services that offer the "cookie-less" solution, albeit not free. But I found one that works best for me: [Plausible](https://plausible.io/).

> Heads up: Legal stuff is hard. IANAL, I'm just a simple person that does not even read Terms & conditions when installing stuff. And... This is not paid writing, I'm just sharing something that works for me.

I choose that platform primarily because it's _open source_. Well, they do have a cloud solution but I choose to [self-host](https://plausible.io/self-hosted-web-analytics) because I already have my cloud instance running for various other projects. Having these options is exactly what I need and also, another reason why I love open source. But don't be mistaken, their cloud solution pricing is reasonable too. Maybe I consider switching to their cloud in the future.

Be warned that, a cookie-less solution may not be for everyone, especially for projects with a large team. For instance, you can't have advanced analytics like retention, heatmap, or A/B testing without putting a cookie or tracker on your website. For small projects, it works great. [Their data policy](https://plausible.io/data-policy) will tell you more about how they collect and store data.

It's nice to tell you why I choose it so far. Now I'll give some screenshots to give you a quick idea of what you'll get using this platform.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657953403699/g_qkiupq_.png align="left")

So the data is stored in the range from "last 12 months" to "realtime" where it's shown graph in minutes, and yes they do reupdate itself without manual refreshing. It's awesome that they can also tell us the unique visitor I had daily.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657953592411/MbdAiS0q7.png align="left")

This is the thing that I liked so far. It shows top sources, top pages visited, country maps, and device lists by whatever graph range you're viewing. You can also choose different sources from the top right of each panel. Seeing these metrics reminds me of a similar thing that Google Analytics do with their basic tracking, but much better as it's not relying on cookies. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657954402663/G0lB9G_3c.png align="left")

So that's it. I put all my project analytics under this platform from now on. It's dead simple to do that. I can't wait to experiment with marketing for my projects!