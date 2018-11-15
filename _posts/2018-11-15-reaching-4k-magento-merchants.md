---
layout: post
title: Reaching 4k Magento merchants
tags: magento security ecommerce
categories:
  - magento
  - security
excerpt_separator: <!--more-->
---

About a month ago, I decided to start a project that has since proved
very challenging. Unlike most projects I work on, this one isn't about
building software, but rather trying to convince people to buy _my_ software
for their own good. I know that sounds pretentious - just keep reading.

<!--more-->

## Background

Over the past two years, I've done a fair amount of contract work for both
merchants and agencies, particularly in the area of malware removal and disaster
recovery. As such, I've seen a lot of exploits, and I've witnessed firsthand how
devastating the aftermath can be for SMBs. The severity of a compromised shop is
not lost on me.

What always shocks me most, however, is how few merchants actually know they have
a problem before it's too late. Most depend on an agency or an individual to keep
up with maintenance, and often times that responsibility is neglected. In the end,
it is the merchant who suffers the consequences, which is why I compel anyone who
runs an ecommerce shop to take an active role in its maintenance and security.

## Outreach

To make merchants aware of potential security risks, while lining my pockets (LOL),
I started an outreach campaign for [Tokenize User Authentication](https://store.nickolasburr.com/tokenize-user-authentication.html)
targeting merchants that met the following criteria:

- Magento 1.x
- Publicly accessible admin login at default `/admin/` URI
- Lack of MFA

These are prime targets for brute-force attacks, so it made sense to start here.

To generate seed data, I used a dockerized version of Wappalyzer in conjunction with
a web crawler, which ran for ~72 hours and logged ~26k detections.

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
people off on the Internet. The entire point of the exercise was to alert merchants of
a major security risk, while promoting a product of mine that would help them address
the underlying problem. That's my story, and I'm sticking to it.
---

## Takeaways

I always try to take something positive from an experience. While I may have felt cheap
and dirty sending unsolicited emails, it was for a noble cause. And as much as I would
love for merchants to adopt and utilize the extension, my only real wish is the email
will reach someone, somewhere, and motivate them to improve security.

The [current state of affairs](https://gwillem.gitlab.io/2018/11/12/merchants-struggle-with-magecart-reinfections/)
for Magento 1.x security is bleak and, without active merchant participation, it will
only continue to worsen.
