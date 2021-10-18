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
    
    a. Make an [Internet Identity](https://identity.ic0.app/) if you do not already have one
    
    b. We recommend you add multiple devices or a recovery method to avoid accidental loss of access

2. Within the NNS Frontend dapp. 
    
    a. First you need to have ICP on your account. Navigate to the `ICP` tab to see your account address, it should look something like this `723cd441238da744a097c3a20f8f4050d8355afb46fe12a1428a63996c37d918` (your address will be a different number). When you transfer ICP to this address, for instance by withdrawing ICP on an exchange where you have bought ICP, it will appear in the NNS Dapp.

    b. Once you have ICP on your account, navigate to the `neuron` tab

c. Click `stake neuron` button and follow the instructions.

3. That's it!

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

If you use the NNS Dapp, you are accepting the following trade-offs and risks:

* Most, but not all devices and browsers support WebAuthn, so the NNS Dapp can sometimes not be used.
* If you only have 1 device tied to your [Internet Identity](https://identity.ic0.app/), and you lose that device, you lose all access. For example, if you have only one iPhone attached as a device to your Internet Identity, you are betting your ICP on it always working. If for instance you only log in via Face ID and the phone no longer recognizes you, you lose access to all your ICP. Similarly, if you misplace your phone or it is stolen, you lose your ICP. You can reduce this risk by adding multiple devices or a recovery mechanism.
* If one of your devices is compromised, your ICP may be stolen. When ICP is staked in a neuron it cannot be immediately transferred but the attacker may steal your rewards and the attacker may set your neuron to dissolve in order to steal the locked ICP. 
* If the Internet Identity or the NNS Dapp are compromised you may lose your ICP. By using them, you are implicitly trusting that the [community-vetted NNS Frontend dapp](https://github.com/dfinity/nns-dapp) is not compromised and that the [community-vetted Internet Identity canister](https://medium.com/dfinity/verifying-the-internet-identity-code-a-walkthrough-c1dd7a53f883) is not compromised.
