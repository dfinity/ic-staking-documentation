---
layout: default
title: 3. Maximum Ease Staking Option
nav_order: 4
# has_children: true
permalink: docs/3-maximum-ease-staking-option
---
Warning: documentation in beta
{: .label .label-red }

{: .no_toc .text-delta }

1. TOC
{:toc}

* * *
# Maximum ease option: How to stake

If you choose to stake with the **maximum ease option**, this chapter is for you. It is a very short chapter.

* * *
## 5 steps to stake 

To recap, the easiest staking option is via the NNS Frontend Dapp.

In **networked smartphone** or **networked computer**, do the following:

1. Log into [NNS Frontend Dapp](https://nns.ic0.app/)
    
    a. Make an [Internet Identity](https://identity.ic0.app/) if you not already have one
    b. Highly recommend you add multiple devices

2. Within NNS Frontend dapp, navigate to the `ICP` tab. Send ICP to an account.
    
    a. Account should look something like this `723cd441238da744a097c3a20f8f4050d8355afb46fe12a1428a63996c37d918`

3. Navigate to the `neuron` tab

4. Click `stake neuron` button and follow instructions.

5. That's it!

You have successfully staked using the NNS Frontend dapp.

* * *
## Decisions you need to make:

### 1. How do you authenticate to Internet Identity?

[Internet Identity](https://identity.ic0.app/) does **not** use passwords and usernames to log in. [Internet Identity](https://identity.ic0.app/) takes advantage of the Web Authentication (WebAuthn) API to provide secure cryptographic authentication. This means that you authenticate by "something you have" (e.g a phone, Yubikey, etc...) instead of "something you know" (e.g. a password).

From the point of view a user, a user would use of the following methods to authenticate:

**1. Computers**

a. Yubikey 
    - with computers with USB ports

b. Thumb print 
    - with computers with electronic fingerprint recognition features like [Touch ID](https://en.wikipedia.org/wiki/Touch_ID)

**2. Smartphones**

a. Face ID 
    - for smartphones with with facial recognition systems

b. Thumb print 
    - for  computers with electronic fingerprint recognition features like [Touch ID](https://en.wikipedia.org/wiki/Touch_ID)

* * *
### 2. If I lose my device, can I still use Internet Identity?

If you have an identity anchor tied to only one device and you lose that one device, you will be locked out. As a best practice, we recommend [adding multiple devices and recovery mechanisms](https://sdk.dfinity.org/docs/ic-identity-guide/auth-how-to.html) to each identity anchor.

* * *
### 3. How do I add more devices to my identity anchor?

To add more devices to an existing identity anchor, [please see the guide here](https://sdk.dfinity.org/docs/ic-identity-guide/auth-how-to.html#_add_a_device).

## Trade-offs and risks

If you use this combination, you are accepting the following trade-offs:

* If you only have 1 device tied to your [Internet Identity](https://identity.ic0.app/), and you lose that device, you lose all access. You should add multiple devices in case one of them malfunctions. For example, if you have only one iPhone attached as a device to your Internet Identity, you are risking your ICP on that iPhone's Face ID always recognizing you. If it cannot, then you lose access to your ICP. Similarly, if you lose your phone, you would lose your ICP.
* Not all devices and browsers support WebAuthn, so this option is sometimes not available.
* You are accepting the risk that the [community-vetted NNS Frontend dapp](https://github.com/dfinity/nns-dapp) is not compromised
* You are accepting the risk that the [community-vetted Internet Identity canister](https://medium.com/dfinity/verifying-the-internet-identity-code-a-walkthrough-c1dd7a53f883) is not compromised
