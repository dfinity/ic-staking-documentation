---
layout: default
title: 3. Easiest staking option
nav_order: 4
# has_children: true
permalink: docs/3-easiest-staking-option
---

# 3. Easiest option
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

# Easiest option: How to stake

If you choose to stake with the **easiest option**, this chapter is for you.

## Decisions you need to make:

### 1. How do you authenticate to Internet Identity?

Internet Identity does **not** use passwords and usernames to log in. Internet Identity takes advantage of the Web Authentication (WebAuthn) API to provide secure cryptographic authentication. This means that you authenticate by "something you have" (ssuch as a phone, yuibkey, etc...) instead of "something you know" (like a password).

From the point of view a user, a user would use of the following methods to authenticate:

**Computer**

* Yubikey
* Thumb print

**Phone**

* Face ID
* Thumb print

### 2. If I lose my device, can I still use Internet Identity?

If you have an Identity Anchor tied to only one device and you lose that one device, you will be locked out. As a best practice, we recommend [adding multiple devices and recovery mechanisms](https://sdk.dfinity.org/docs/ic-identity-guide/auth-how-to.html) to each Identity Anchor.

### 3. How do I add more devices to my Identity Anchor?

To add more devices to an existing Identity Anchor, [please see the guide here](https://sdk.dfinity.org/docs/ic-identity-guide/auth-how-to.html#_add_a_device).

## Trade-offs and risks

If you use this combination, you are accepting the following trade-offs:

* If you only have 1 device tied to your Internet Identity, and you lose that device, you lose all access. You should add multiple devices in case one of them malfunctions. For example, if you have only one iPhone attached as a device to your Internet Identity, you are risking your ICP on that iPhone's Face Id always recognizing you. If it cannot, then you lost access to your ICP. Similarly, if you lose your phone, you would lose your ICP.
* Not all devices and browsers support WebAuthn, so this option is sometimes not available.
* You are accepting the risk that the [community-vetted NNS Front End Dapp](https://github.com/dfinity/nns-dapp) is not compromised
* You are accepting the risk that the [community-vetted Internet Identity canister](https://medium.com/dfinity/verifying-the-internet-identity-code-a-walkthrough-c1dd7a53f883) is not compromised
