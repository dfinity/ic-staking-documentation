---
layout: default
title: 4. Safest staking option
nav_order: 5
has_children: true
permalink: docs/safest-staking-option
---

# 4. Safest option: How to stake

There are two basic options you can take if you choose this option:

    1. **Air gapped** computer + **networked** phone
    2. *Coming Soon*: **[Ledger Nano](https://shop.ledger.com/products/ledger-nano-x) integration** 

    **The Risks involved**

    There are various artifacts that can be derived from your `seed phrase`.The diagram below explains which are derived and the risks from each artifact.

    ![image](../assets/images/seed-phrase-risks.png)

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

            [![Ledger Nano](https://img.youtube.com/vi/=YefRR6O-xjg/0.jpg)](https://www.youtube.com/watch?v=YefRR6O-xjg)

If you choose to stake with the **safest option**, this chapter is for you.

This section is for people who chose to stake by custodying their own `seed phrase`

As a reminder, there are three basic steps (whose implementation depend on the technology you choose):

**To stake, there are three steps:**

1. Generate a **private key** 
    *This step would only happen once 1️⃣ per cold wallet. For most people, this means you will do this step only once.*

2. Create a **neuron** with a **dissolve delay** 
    *This step would only happen once 1️⃣ per cold wallet. For most people, this means you will do this step only once.*

3. *Optional*: Add more ICP to the Neuron (“top up the neuron”) 
    *This step could happen many times 🔁 per neuron.*

This chapter explains how to accomplish these steps given one self-ustodies their own `seed phrase`.