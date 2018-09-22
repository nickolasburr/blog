---
layout: post
title: Magento 1.x Threat Vectors and Remediation Tactics
tags: magento security ecommerce
categories:
  - magento
  - security
excerpt_separator: <!--more-->
---

Magento is the quintessential target for credit card theft.
That might seem obvious, but the reasons why are actually
complicated and multifactorial, so I'll spare the details
for a different post. For the purpose of this post, just
understand that Magento is an especially targeted platform
for credit card fraud.

<!--more-->

## Background

Data breaches can be very costly, especially for PCI-compliant
merchants rated between levels 1-3. In an era marked by newsreel
data breaches and public outcry over privacy concerns, it is, now
more than ever, the compulsory duty of online merchants to make
the investment in an intelligent, reliable, and dedicated Magento
hosting provider. Merchants who try to take shortcuts and save
a few extra dollars now _always_ end up regretting that decision
down the road. Don't pay for free lessons.

## Introduction

There are several common threat vectors that have been used
over the years to exploit Magento. For many of these attack
types, the only way to mitigate the problem is to patch the
application. However, there exists a subset of all exploits
that rely on one or more weak aspects of the environment in
order for the vulnerability to be exploitable.

By hardening the environment around Magento, you can effectively
eliminate certain attack types, sacrificing little or nothing as
a consequence. Such an approach is especially useful for high-risk,
high-volume storefronts that prioritize availability, usability,
and security.

I'm going to walk through a few popular attack types, and show how
simple countermeasures can potentially save your Magento storefront
from falling prey to the malevolent neckbeards.

## Admin brute-force attacks

> A brute force attack is a trial-and-error method used to obtain
> information, such as a user password or personal identification
> number (PIN).

__Threat__: Successful brute-force attacks give an unauthorized
individual administrative access, which can include access to
sensitive information like payment gateway credentials, customer
and order information, ERP system credentials, and much, much more.

This particular attack is common under the following conditions:

- Default/weak front name for administrative panel
- Default administrator username
- Weak password requirements
- Lack of access and activity monitoring

__Mitigation__: Effectively managing brute-force attacks is probably
the easiest type of attack to mitigate. As an example, by using the
following tools (or any of their variants), you can develop a more
transparent monitoring system that will put you in a better position
to handle brute-force attacks at both the network and application level.

Techniques and tools I use include:

- Strong front name for administrative panel
- Strong password requirements<sup>1</sup>
- Admin access and activity monitoring
  + [Admin Actions Log](https://amasty.com/admin-actions-log.html)
- Multifactor Authentication
  + [Two-Factor Authentication](https://amasty.com/magento-two-factor-authentication.html)
- Server and application monitoring
  + [Stackdriver Monitoring](https://cloud.google.com/monitoring/)
- Cloud proxy service
  + [Cloudflare](https://www.cloudflare.com)
  + [Akamai](https://www.akamai.com)

## XSS attacks

> Cross-site scripting (XSS) attacks are a type of injection, in
> which malicious scripts are injected into otherwise benign and
> trusted websites.

There are two types of XSS attacks:

- Persistent XSS attacks
- Reflected XSS attacks

To keep things simple, we'll focus on persistent XSS attacks.

__Threat__: Due to an XSS vulnerability in Magento, an attacker
injected an HTML `<script>` tag into a database table that loads
a malicious JavaScript file from a remote server when a user visits
the website.

__Mitigation__: The best mitigation strategy for these types of
attacks is to use [CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)
and whitelist what origins JS files can be loaded from. It will
prevent the browser from loading the JS file, protecting the user
and giving you time to apply the appropriate patch(es), and clean
the database table.

## Input Validation

> Input validation, also known as data validation, is the proper
> testing of any input supplied by a user or application. Input
> validation prevents improperly formed data from entering an
> information system.

__Threat__: Due to an unsanitized input field, an attacker was able
to execute arbitrary PHP code on the server, modifying Magento core
to send all credit card transactions to a remote server.

__Mitigation__: This type of attack is moderately defensible. While
execution of malicious PHP code can result in sensitive information
being leaked, this vector can be minimized greatly with a strong
understanding of Unix-based filesystem permissions and a dash of
creativity.

__Warning__: This is one specific area where I fervently disagree
with the Magento Inc. recommended approach, so take my approach at
face value. It's battle-tested and has saved my rear many a time.

###### Harden File Permissions

Magento only requires write access to a small subset of directories,
such as `var` and `media`. Since the webserver runs as an unprivileged
user like `apache`, `nginx`, or `www-data`, any malicious code executed
as the result of an input validation exploit would also be ran as that
user. Likewise, setting the owner and group of all files and directories
to a privileged user, with the exception of `var` and `media`, would make
those files and directories unwritable by the webserver user.

###### e2fsprogs

Another tactic is to use `e2fsprogs`, particularly `chattr`. In addition
to hardening file permissions, you can use extended filesystem attributes
to prevent manipulation of files and directories. This is particularly
useful because to modify an inode's attributes requires elevated privileges,
which the webserver user is lacking.

###### Train of thought

The main reason why I'm so adamantly against the Magento Inc. approach is
because it gives the webserver user write access to core files, something
it shouldn't have. The webserver user only needs read access to core files,
so when you give it write access, you're opening yourself up to issues that
are otherwise preventable.

## Magento Security Best Practices

In addition to what I've outline above, Magento provides a nicely
detailed guide on security best practices, which you can find [here](https://magento.com/security/best-practices/security-best-practices).

## Footnotes

1. The most common counterargument I hear to enforcing stronger
passwords is that they're impossible to remember, which causes
employee frustation. My recommendation is this: encourage them
to use a password manager. As an example, Chrome has an excellent
password manager built into it, and it's extremely easy to use.
The same goes for Firefox and any other major browser.
