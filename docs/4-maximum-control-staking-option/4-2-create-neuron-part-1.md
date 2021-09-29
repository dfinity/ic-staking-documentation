---
layout: default
title: 4.2 Create neuron with dissolve delay (Part 1)
parent: 4. Maximum Control Staking Option
---

{: .no_toc .text-delta }

1. TOC
{:toc}

* * *
# 4.2 Create a **neuron** with a **dissolve delay**
## Part 1 of 3: Air-gapped computer

*This step is only done once per neuron.*

*Note: To “stake ICP” and to “create a neuron” are the same activity so they are used interchangeably.*

This section assumess you successfully installed the the QR tools on your **air-gapped computer** from 4.0.

In this section, we need to "bridge the air gap." This means that we will continue to perform the sensitive operations within the **air-gapped computer**, but we will use a **networked smartphone**'s QR code scanner to send the messages from **the air-gapped computer** to the Internet Computer.

![image](../assets/images/qr-code-scan-2.png)

* * *
## 4.2.1 Send ICP to your `ledger account number`

This account number lives in the Ledger canister that maintains the ICP addresses for the entire network. This account number is analogous to "addresses" in other blockchains. You need to send the ICP you want to stake to the `ledger account number`. In our case, the `ledger account number` from 4.1 was `77b5eb9a465f4ce6f4da494ee2bfedeefe0b52d106e0272556c1ad991f99e3da` so that is the address we will use.

To create a neuron, you need to stake a minimum of 1 ICP. Anything less will *not* create a neuron.

**If you cannot send ICP to your ledger account number, do not continue.** Try again, check out support, or submit a question to support.

* * *
## 4.2.2 Generate a signed message to "create a neuron" using `quill`

You will use `quill`'s  `neuron-stake` command of the form:

On the **air-gapped computer**:

```bash
// This is just the structure, copy/pasting WILL NOT work. See below for working command
$ target/release/quill --pem-file private.pem neuron-stake --name $NAME --amount $AMOUNT
```

For this command, the `$NAME` is an arbitrary string, up to 8 characters, that you can use to identify your neuron for the purposes of topping up later with `quill`. For example, if you intend to have only one eight-year neuron, you could use the name `8yneuron`. This string has no meaning otherwise, and will not be visible anywhere else. You can store this on your **air-gapped computer.**

The `$AMOUNT` should not include the transaction fee, but remember that it will still be deducted from your account, so if you wish to stake everything you've got, stake your balance minus the 0.0001 ICP fee.

Here is the same command with the fields `$NAME` (“neuron3”) and `$AMOUNT` (1.01) filled out, but you should choose your own fields.

On the **air-gapped computer**:

```bash
// Create the message that tells IC "create the neuron" and save it "message.json"
$ target/release/quill --pem-file private.pem neuron-stake --name neuron3 --amount 1.01 > message.json
```

