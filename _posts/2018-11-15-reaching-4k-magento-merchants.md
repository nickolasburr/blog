---
layout: post
title: Reaching 4K vulnerable Magento merchants
tags: magento security ecommerce
categories:
  - magento
  - security
redirect_from: "/magento/security/2018/11/15/reaching-4k-magento-merchants.html"
excerpt_separator: <!--more-->
---

About a month ago, I decided to start a new project, and it has since proven
to be quite challenging. Unlike most projects I work on, this one isn't about
building software, but rather trying to convince people to buy software for
their own good. Sounds like a scam, right?

<!--more-->

## Background

Let me start by giving some context. Over the past two years, I've done a fair
amount of contract work for both merchants and agencies, particularly in the areas
of malware removal and disaster recovery. I've seen a lot of exploits, and I've
witnessed firsthand how devastating the aftermath can be for SMBs. The severity
of a compromised shop is not lost on me.

What always shocks me most, though, is how few merchants actually know they have
a problem before it's too late. Most depend on an individual or an agency to keep
up with maintenance, and often times that responsibility is neglected. In the end,
it is the merchant who suffers the consequences, which is why I compel anyone who
runs an ecommerce shop to take an active role in its maintenance and security.

## Outreach Campaign

In the past, I've written about [brute-force attacks](https://blog.nickolasburr.com/magento/security/2018/10/17/magento-brute-force-attacks.html)
as a means to shine light on a very real issue that _still_ affects Magento in 2018.
However, we're now at a point where [credit card theft is reaching new levels](https://gwillem.gitlab.io/2018/08/30/magentocore.net_skimmer_most_aggressive_to_date/),
and it's only going to get worse. That is, unless merchants take control and begin
to push back.

To do my part, I wanted to make merchants very aware of the real threats they
face in regards to credit card theft, so I decided to start an outreach campaign
for [Tokenize User Authentication](https://store.nickolasburr.com/tokenize-user-authentication.html),
which is an extension I sell that helps mitigate brute-force attacks.

As a starting point, I wanted to identify merchants with the following criteria:

- Magento 1.x
- Publicly accessible admin login at default `/admin/` URI
- Lack of MFA

These are prime candidates for brute-force attacks, so it made sense to start here.

To generate seed data, I used a dockerized version of [Wappalyzer](https://www.wappalyzer.com)
in conjunction with [scrapy](https://scrapy.org), which ran for ~48 hours and logged ~26k detections.

To actually begin the outreach process, however, I had to sift through garbage. There
were tons of false positives, abandoned websites, staging websites, portal websites,
etc. that weren't applicable. Once I finished sifting, I got the list down to ~4k
seemingly relevant, legitimate, vulnerable Magento 1.x shops.

```
wc -l m1.csv
# 3986 m1.csv
```

I was now at a point where I could start sending emails, but I didn't have any. And
there's no faster way to get blacklisted than to send 4,000 emails to `info@domain.tld`.
With CAN-SPAM laws and Gmail limits fencing me in, my only solution was to break the
list into chunks, find the proper business email (semi) manually, and send the emails
in daily blasts of 100.

---

At this point, I want to highlight that I'm not some skeevy email spammer trying to rip
people off on the Internet. The main purpose of the exercise was to alert merchants of
a major security risk, while promoting a product of mine that would help them address
the underlying problem. Some people might find that distasteful, but that's capitalism,
baby.

---

Unsurprisingly, I've received very few responses, most of which either say "No, thanks"
or "Stop spamming me, as@$&le". Thankfully, I'm nearing the end of the campaign and I
couldn't be more excited.

## Takeaways

I always try to take something positive from an experience. While I may have felt cheap
and dirty sending unsolicited emails, it was for a noble cause. And, as much as I would
love for merchants to adopt and utilize the extension, my only real wish is the email
will reach someone, somewhere, and motivate them to improve security, because the
[current state of affairs](https://gwillem.gitlab.io/2018/11/12/merchants-struggle-with-magecart-reinfections/)
is rather bleak and, without active merchant participation, it will only continue to
worsen. I've done my part, and I hope others will do theirs.
