---
layout: default
title: 4.2 Create neuron with dissolve delay (Part 2)
parent: 4. Safest Staking Option
---

{: .no_toc .text-delta }

1. TOC
{:toc}

* * *
# 4.2 Create a **neuron** with a **dissolve delay** 
## Part 2 of 3: Bridge the air-gap


This section walks you through the tools necessary to bridge the air gap between your **air-gapped computer** and the **networked smartphone**.

## 4.2.3 Bridge the Airgap: Send the message to the Internet Computer using a QR code

Since your **air-gapped computer** is not connected to the internet, we will use a **QR app** to send the message generated in 4.2.1 to the Internet Computer. We will use `IC Transaction Scanner` which lives in a canister (and whose code is visible here: [https://github.com/ninegua/ic-qr-scanner](https://github.com/ninegua/ic-qr-scanner))

![image](../assets/images/qr-code-scan-2.png)

* * *
### 4.2.3a Convert the `message.json` into QR codes

`message.json` file actually has multiple messages for the Internet Computer, so you will run a script that will put you in the following loop:

1. You run script
2. QR code is generated
3. You scan QR code with your smartphone
4. Hit ENTER and return to step 2

The command will break up all the messages in `message.json` into QR codes you will scan sequentially in step 2.2

![image](../assets/images/qr-code.png)

* * *
### 4.2.3b Navigate your smartphone to `IC Transaction Scanner` and scan the QR code: 

On your **networked smartphone**, navigate to URL for `IC Transaction Scanner`: [https://p5deo-6aaaa-aaaab-aaaxq-cai.raw.ic0.app](https://p5deo-6aaaa-aaaab-aaaxq-cai.raw.ic0.app/)

* * *
### 4.2.3c Scan QR code from your air-gapped terminal

We will scan the QR code so your **networked smartphone** sends the message written in the **air-gapped computer.**

**Scan code**

<!-- ![image](../assets/images/ic-transaction-scan.png) -->
<img src="../assets/images/ic-transaction-scan.png" alt="drawing" width="300"/>

**Press `Send` to send message to the Internet Computer**

<!-- ![image](../assets/images/ic-transaction-scan-send.png) -->
<img src="../assets/images/ic-transaction-scan-send.png" alt="drawing" width="300"/>

* * *
### 4.2.3d Press ENTER on terminal to get the next QR code

Repeat step 4.2.3c if there are any other QR codes

🎉🎉 **Success**! ***Neuron created!*** 🎉🎉

You will get a response on  **`IC Transaction Scanner`** that confirms the neuron was successfully created. ****You will get a `neuron id`. A `neuron id` will look come back to you as a response that looks like this:

```jsx
(
  record {
    result = opt variant {
      NeuronId = record { id = 5_241_875_388_871_980_017 }
    };
  },
)
```

In the example above, the neuron id is `5241875388871980017`

You can view your neuron on community dashboards like [ic.rocks](http://ic.rocks) by going to URL: [https://ic.rocks/neuron/](https://ic.rocks/neuron/3028){{neuron-id}}

For example, neuron `5241875388871980017` [https://ic.rocks/neuron/5241875388871980017](https://ic.rocks/neuron/5241875388871980017)

![image](../assets/images/ic-rocks-neuron.png)

* * *
## 4.2.4 Outcome

In this section, we did a few things, so let’s recap what we did and where we should be before moving forward.

**If you do not end up with a table that looks like the one below, do not continue**. Try again, check out support, or submit a question to support.

In addition to the artifacts in [previous section](../4-safest-staking-option/4-2-create-neuron-part-1.md), you should have:

| Artifact | Example | Security| Final outcome| Storage |
| ------------- | ------------- | | ------------- | | ------------- | | ------------- |
| `neuron id` | `5241875388871980017`| • If someone has this, they can see your balance.  <br /> • If you lose this, you can reconstruct it. | • You generated this in 4.2.2. | to remain on air-gapped computer |
| `neuron name` | `neuron3` | • If someone has this, it gives them nothing.<br /> • If you lose this, you can get it back. | • You generated this in 4.2.3. | to remain on air-gapped computer |
