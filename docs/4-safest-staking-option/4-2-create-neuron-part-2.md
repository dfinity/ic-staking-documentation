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
By now we should have the following:

| Artifact | Example | Security| Final outcome|
| ------------- | ------------- |
| `seed phrase` | `stove reject elder top dentist car suit license grid uncle ape wash`| • If someone has this, they can take your tokens. <br /> • If you lose it, you can lose access to your ICP. <br /> • You can keep this if you want to be able to generate your private key again. | • You created this via Keysmith in this section in 4.1.1.  <br />• You will have properly stored in 4.1.4<br />• You deleted this from your computer in 4.1.5|
| `private key` | ```-----BEGIN EC PARAMETERS----- ``` (and continues...) | • If someone has this, they can take your tokens. <br /> • If you lose it, you can recreate from seed phrase <br /> | • You created this via Keysmith in this section in 4.1.2. |
| `ledger account number` | `77b5eb9a465f4ce6f4da494ee2bfedeefe0b52d106e0272556c1ad991f99e3da`| • If someone has this, they can view your token balance. <br /> • If you lose it, you can go through steps to get it back with your private key. | • You generate this in 1.3. This can be stored anywhere.|
| `neuron id` | `5241875388871980017`| • If someone has this, they can see your balance.  <br /> • If you lose this, you can reconstruct it. | • You generated this in 4.2.2. This can be stored anywhere.|
| `neuron name` | `neuron3` | • If someone has this, it gives them nothing.<br /> • If you lose this, you can get it back. | • You generated this in 4.2.3. This can be stored anywhere.
