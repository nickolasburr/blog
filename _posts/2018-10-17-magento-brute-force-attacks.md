---
layout: post
title: Magento brute-force attacks
subtitle: And what you can do to fight back
tags: magento security ecommerce
categories:
  - magento
  - security
excerpt_separator: <!--more-->
---

Brute-force attacks have long plagued Magento security. In terms of credit card
theft, it's one of the most successful and widely used attack vectors, and has
resulted in [thousands of compromised stores](https://gwillem.gitlab.io/2018/08/30/magentocore.net_skimmer_most_aggressive_to_date/)
over the past few years.

<!--more-->

I briefly discussed brute-force attacks in a [previous post](https://blog.nickolasburr.com/magento/security/2018/09/21/magento-1x-threat-vectors-remediation-tactics.html),
but I want to dive deeper and answer the following questions:

1. What is a brute-force attack?
2. Why are brute-force attacks so effective?
3. What can I do to protect my store?

## What is a brute-force attack?

Contrary to those ridiculous Hollywood scenes with a person in a black hoodie hunched
over a laptop in a dark room, the overwhelming majority of cyber attacks in 2018 are
programmatic. As in, the attackers are efficient and use software to find and exploit
vulnerabilities in software.

Like the name suggests, brute-force attacks use trial and error to gain access
to an account. In most cases, an attacker will utilize a set of common and/or
default usernames and passwords to expedite the process. This is known as a
dictionary attack, and has proven widely effective against Magento.

## Why are brute-force attacks so effective?

**Lack of monitoring**

> Effective monitoring requires effective tools and planning, which requires knowledge,
> time, and money.

The problem is two fold. Magento doesn't provide a lot of transparency in regards to
user activity, so in order to get this information from within Magento, you need an
extension. The only well-established options are premium, so it's an expense. To get
similar information from outside of Magento (e.g. proxy service like Cloudflare, Akamai),
you need to create an account with the provider, update DNS, wait for DNS changes, set up
monitoring rules (e.g. page rules in Cloudflare), and more, just to get started. It can
feel tedious and overwhelming for many people.

**Defaults**

When it comes to Magento administration, using any of the defaults (sans admin panel URI, IMHO)
is strongly discouraged. If you're using a username like `admin` or `admin1`, chances are you're
probably not super picky about passwords either. This is where most of the success happens.

**Weak password requirements**

This goes along with #2, insofar as it simplifies the brute-force attacking process. Cracking
passwords is an exponential problem, so short, weak passwords make the process exponentially
faster.

## What can I do to protect my store?

Since we're talking about brute-force attacks specifically, let's focus in on those products
for Magento. Below are options for anyone looking to better protect both customer and admin
accounts:

+ [Two-Factor Authentication](https://amasty.com/magento-two-factor-authentication.html) (MFA, Amasty)
+ [Tokenize User Authentication](https://store.nickolasburr.com/tokenize-user-authentication.html) (TOTP, yours truly)

For monitoring admin activity and connections:

+ [Admin Actions Log](https://amasty.com/admin-actions-log.html)
+ [Cloudflare](https://www.cloudflare.com) with Page Rules for the admin panel URI

This list is not exhaustive by any means, but it's a starting point. Using any of the tools
above will put you in a better spot to secure your store. However, it's up to you to take
the initiative.
