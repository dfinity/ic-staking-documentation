---
layout: page
title: 2. Tool options
permalink: /tools/
---

# 2. Tool options

To stake, you have many options, each with different security and usability trade-offs. Choosing your setup is usually where people get most stuck. 

This chapter summarizes your options from **easiest** to **safest**.

### Easiest Option

- **Use [Internet Identity](https://medium.com/dfinity/internet-identity-the-end-of-usernames-and-passwords-ff45e4861bf7) with the [NNS frontend dapp](https://nns.ic0.app/)**

    *I**nternet Identity***                                                         

    ![Screen Shot 2021-09-16 at 4.49.01 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/62b73380-b2f2-411e-9814-96ca2ec73159/Screen_Shot_2021-09-16_at_4.49.01_PM.png)

    ***NNS Frontend Dapp***

    ![Screen Shot 2021-09-16 at 4.47.56 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e78ad183-bae5-4840-a421-aaa36bdca1b0/Screen_Shot_2021-09-16_at_4.47.56_PM.png)

    **Traits**

    - Most convenient. Entirely web-based. No need to download or install anything.
    - NNS Dapp has all the functionality you need
    - This is a very common method

    **Decisions you need to make:**

    - 1. **How do you authenticate to Internet Identity?**

        Internet Identity does **not** use passwords and usernames to log in. Internet Identity takes advantage of the Web Authentication (WebAuthn) API to provide secure cryptographic authentication.

        From the point of view a user, a user would use of the following methods to authenticate:

        **Computer**

        - Thumb print
        - Yubikey

        **Phone**

        - Face ID
        - Thumb print
    - 2. **If I lose my device, can I still use Internet Identity?**

        If you have an Identity Anchor tied to only one device and you lose that one device, you will be locked out. As a best practice, we recommend [adding multiple devices multiple devices and recovery mechanisms](https://sdk.dfinity.org/docs/ic-identity-guide/auth-how-to.html) to every Identity Anchor.

    - 3. **How do I add more devices to my Identity Anchor?**

        To add more devices to an existing Identity Anchor, [please see the guide here](https://sdk.dfinity.org/docs/ic-identity-guide/auth-how-to.html#_add_a_device).

    **Trade-offs and risks**

    If you use this combination, you are accepting the following trade-offs:

    - If you only have 1 device tied to your Internet Identity, if you lose that device, you lose access. You should add multiple in case a device malfunctions. For example, if you have only one iPhone attached as a device to your Internet Identity, you are risking your ICP that the iPhone's Face Id would always recognize you. If it cannot, then you lost access to your ICP. Similarly, if you lose your phone, you would lose your ICP.
    - Not all devices and browsers support WebAuthn, so this option is sometimes not available.
    - You are accepting the risk that the [community-vetted NNS Front End Dapp](https://github.com/dfinity/nns-dapp) is not compromised
    - You are accepting the risk that the [community-vetted Internet Identity canister](https://medium.com/dfinity/verifying-the-internet-identity-code-a-walkthrough-c1dd7a53f883) is not compromised

### Safest Option

- Use your `seed phrase` directly with a few options for self-custody tools.

    This option is not as easy. It is less prone to software-based compromise (e.g. if you use Internet Identity on only phone and your phone dies) if you protect your `seed phrase`, which puts the ***risk on you*** to protect your seed phrase well. This option is also a bit more technical. This is the *safest* option from a software point of view because you are relying on less software surface area, but it is the *riskiest* from a human point of view in that it puts the risk of your `seed phrase` custody on you.

    There are two basic options you can take if you choose this option:

    1. **Air gapped** computer + **networked** phone
    2. *Coming Soon*: **[Ledger Nano](https://shop.ledger.com/products/ledger-nano-x) integration** 

    ### **The Risks involved**

    There are various artifacts that can be derived from your `seed phrase`.The diagram below explains which are derived and the risks from each artifact.

    ![Screen Shot 2021-09-16 at 5.24.16 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/70c37fe4-a9e8-493a-b2c8-a1d3a14b56c4/Screen_Shot_2021-09-16_at_5.24.16_PM.png)

    **Red Boxes**

    - 12-word `seed phrase`
    - `Private key`

    If you lose these, you lose access to your ICP

    If someone gets these, they may take your ICP

    **Yellow Boxes**

    - `Public Key`
    - `Principal`
    - `Neuron Id`
    - `Account Id`
    - `Neuron Account`

    If you lose these, you can regenerate them from your seed phrase

    If someone gets these, they can see how ICP you have or your transactions

    **Decisions you need to make**

    - 1. Where to store your `seed phrase`?

        Do **NOT** store your seed phrase electronically. We recommend you store in any of the following options:

        1. Paper
        2. Steel wallets like [Billfodl](https://privacypros.io/products/the-billfodl/)

            ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dd62bd08-e247-4af0-8eb7-9b71ed38c6f4/Untitled.png)

    - 2. Once you have your `seed phrase`, what **tools** can you stake with?

        Right now, your safest option is:

        - 2.1 **Air gapped** computer + **networked** phone
            1. **An air gapped computer**
                1. [Keysmith](https://github.com/dfinity/keysmith) command line tool installed
                2. [Quill](https://github.com/dfinity/quill) command line tool installed

                Air gapped computer will create and sign messages w*hich it cannot send since computer* is air gapped. These messages will be turned into QR codes.

            2. **A networked smart phone**

                Smart phone will "bridge the air gap" by reading QR codes from the air gapped computer and sending them directly to the Internet Computer. The worst security case scenario is that the Phone does not send the messages, but the phone never gets access to the anything sensitive.

                - Smart phone's browser should be at this URL: [https://p5deo-6aaaa-aaaab-aaaxq-cai.raw.ic0.app/](https://p5deo-6aaaa-aaaab-aaaxq-cai.raw.ic0.app/)
                - Note: Incorporate the “[bridging the airgap”](https://docs.google.com/document/d/1chBtL7rTEqPeZ4E04-IXMO0ixZZ98bOPSUxzt5TLZSs/edit#heading=h.kvf3xrirsmls) section by Jan

        But soon, you will have another option:

        - 2.. *Coming Soon*: **[Ledger Nano](https://shop.ledger.com/products/ledger-nano-x) integration**

            For Ledger Nano integration you will need the following:

            1. **A networked computer**
                1. "Ledger's Internet Computer" command line tool installed
                2. Browser authenticated to [NNS FE Dapp](https://nns.ic0.app/#/auth) 
            2. **A Ledger Nano**

            [https://www.youtube.com/watch?v=YefRR6O-xjg](https://www.youtube.com/watch?v=YefRR6O-xjg)