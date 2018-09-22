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
for a different post. For the sake of this post, understand
that Magento is an especially targeted platform by credit
card fraudsters.

<!--more-->

## Background

There are several common threat vectors that have been used
over the years to exploit Magento. For many of these attack
types, the only way to mitigate the problem is to patch the
application. However, for several of these exploits, aspects
of the environment must also be weak for a vulnerability to
be exploitable.

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

#### Threat

Successful brute-force attacks give an unauthorized individual
administrative access, which can include access to sensitive
information like payment gateway credentials, customer and order
information, ERP system credentials, and much, much more.

This particular attack is common under the following conditions:

- Default/weak front name for administrative panel
- Weak user password requirements
- Lack of access and activity monitoring

#### Mitigation

Effectively managing brute-force attacks is probably the easiest
type of attack to mitigate. By using the following tools (or any
variants), you will place yourself in a better position to handle
brute-force attacks at both the network and application level.

- Strong front name for administrative panel
- Strong user password requirements
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

#### Threat

Due to an XSS vulnerability in Magento, an attacker injected
an HTML `<script>` tag into a database table that loads a
malicious JavaScript file from a remote server when a user
visits the website.

#### Mitigation

The best mitigation strategy for these types of attacks is to
use [CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)
and whitelist what origins JS files can be loaded from. It will
prevent the browser from loading the JS file, protecting the user
and giving you time to apply the appropriate patch(es), and clean
the database table.

## Input Validation

> Input validation, also known as data validation, is the proper
> testing of any input supplied by a user or application. Input
> validation prevents improperly formed data from entering an
> information system.

#### Threat

Due to an unsanitized input field, an attacker was able to execute
arbitrary PHP code on the server, modifying Magento core to send
all credit card transactions to a remote server.

#### Mitigation

This type of attack is moderately defensible. While execution of
malicious PHP code can result in sensitive information being leaked,
you can minimize scope and damage by setting rigid permissions on
the underlying filesystem.
