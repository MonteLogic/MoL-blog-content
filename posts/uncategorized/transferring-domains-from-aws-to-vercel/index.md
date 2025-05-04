---
title: "Transferring Domains from AWS to Vercel"
date: "2024-07-26"
---

Although DNS records take a while, from my experience working with Vercel if you do it right it should transfer within 30 minutes.

Set the name server:

```
ns1.vercel-dns.com
```

```
ns2.vercel-dns.com
```

But what record type would it be?

For figuring out nameservers within Route 53, this [forum thread](https://community.cloudflare.com/t/properly-changing-nameservers-on-route53/418135) the is good.

A part of [this video](https://youtu.be/JRZiQFVWpi8?si=5KzaYWUqdzC3KbCw) is helpful too.

...

The migration from AWS to Vercel is taking a particularly long time but it is propagating. I am using this [tool](https://www.whatsmydns.net/#A/), to check if the A name is propagating.

...

When working with the A name, I've noticed it works if you delete every DNS record and then add the A name record provided by Vercel.
