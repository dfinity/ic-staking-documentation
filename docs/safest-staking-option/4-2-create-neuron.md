---
layout: default
title: 4.2 Create neuron with dissolve delay
parent: 4. Safest staking option
---

## 2. Create a **neuron** with a **dissolve delay**

*This step would only happen once 1️⃣ per neuron.*

In this section, we need to "bridge the air gap." This means that we will continue to perform the ***sensitive*** operations within the **air-gapped computer**,  but we will use a **smartphone** QR code scanner to send the messages *from* **the air-gapped computer** t*o the* Internet Computer.

![Screen Shot 2021-09-20 at 12.32.13 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5092c5cc-09d6-48e1-af0c-caa531ae0f56/Screen_Shot_2021-09-20_at_12.32.13_PM.png)

To QR encode your message, you should install `qrencode` (or similar) on your **air-gapped computer.** 

Installation steps:

- OSX: [https://formulae.brew.sh/formula/qrencode](https://formulae.brew.sh/formula/qrencode)
- Debian package on Ubuntu: TB

### 2.1 Generate a signed message to "create a neuron" using `Quill`

**Note**: *To “stake ICP” and to “create a neuron” are the same activity so they are used interchangeably.*

You will use **`quill**neuron-stake` command of the *form*:

```jsx
// This is just the structure, copy/pasting WILL NOT work. See below for working command
quill --pem-file private.pem neuron-stake --name $NAME --amount $AMOUNT
```

For this command, the `$NAME` is an arbitrary string, **up to 8 characters**, that you can use to identify your neuron for the purposes of topping up later with `Quill`. For example, if you intend to have only one eight-year neuron, you could use the name `8yneuron`. This string has no meaning otherwise, and will not be visible anywhere else. **You should store this.**

The `$AMOUNT` should not include the transaction fee, but remember that it will still be deducted from your account, so if you wish to stake everything you've got, stake your balance minus the 0.0001 ICP fee.

Here is the same command with the fields `$NAME` (“neuron3”) and `$AMOUNT` (1.01) filled out. 

**You should choose your own fields.**

Inside the **air-gapped computer**:

```bash
// Create the message that tells IC "create the neuron" and save it "message.json"
$ quill --pem-file private.pem neuron-stake --name neuron3 --amount 1 > message.json
```

### 2.2 Send the message to the Internet Computer using a QR code

Since your **air-gapped computer** is not connected to the internet, we will use a **QR app** to send the message generated in 2.1 to the Internet Computer. We will use `IC Transaction Scanner` which lives in a canister (and whose code is visible here: [https://github.com/ninegua/ic-qr-scanner](https://github.com/ninegua/ic-qr-scanner))

![Screen Shot 2021-09-20 at 12.32.13 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5092c5cc-09d6-48e1-af0c-caa531ae0f56/Screen_Shot_2021-09-20_at_12.32.13_PM.png)

**2.2.1 Convert the `message.json` into QR codes**

`message.json` file actually has multiple messages for the Internet Computer, so you will run a script that will put you in the following loop:

1. You run script
2. QR code is generated
3. You scan QR code with your smartphone
4. Hit ENTER and return to step 2

Copy the bash script you will use: [https://github.com/IvanMalison/quill-qr/blob/master/quill-qr.sh](https://github.com/IvanMalison/quill-qr/blob/master/quill-qr.sh)

```bash
// Using "message.json", create QR codes you can scan with your phone
$ bash ./quill-qr.sh < message.json
```

The command will break up all the messages in `message.json` into QR codes you will sca sequentially in step 2.2

![Screen Shot 2021-09-20 at 2.41.29 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/453627a4-6813-4b68-91f2-96968404edb1/Screen_Shot_2021-09-20_at_2.41.29_PM.png)

**2.2.2. Navigate your smartphone to `IC Transaction Scanner`** **and scan the QR code**: 

- **2.2.2a** URL for **`IC Transaction Scanner`:** [https://p5deo-6aaaa-aaaab-aaaxq-cai.raw.ic0.app](https://p5deo-6aaaa-aaaab-aaaxq-cai.raw.ic0.app/)
- **2.2.2b** Scan QR code on your terminal with your smartphone and send it to the IC
    - **Scan code**

        ![Image from iOS (1).png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fd062a3a-5956-4d82-bbad-aa7252deaec3/Image_from_iOS_(1).png)

        - **Press `Send` to send message to the Internet Computer**

        ![Image from iOS (2).png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9cb1936a-eb66-45b0-af1b-470cfd2a21a3/Image_from_iOS_(2).png)

- **2.2.2c** Press ENTER on terminal

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

![Screen Shot 2021-09-20 at 1.16.48 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f00f7ab9-14f8-43cc-b078-561eaea5c74b/Screen_Shot_2021-09-20_at_1.16.48_PM.png)

### **2.3 Send a message to the neuron to “start dissolve delay”**

To increase the dissolve delay of a neuron whose id is `$NEURON_ID`, we will use a command of the form:

```bash
// This is just the structure, copy/pasting WILL NOT work. See below for working command
$ quill --pem-file private.pem neuron-manage $NEURON_ID --additional-dissolve-delay-seconds $SECONDS
```

This shows the `neuron-manage` subcommand, which is used to manipulate neurons after they have been staked as in **2.2**. In this case, we are adding `$SECONDS` seconds to the delay time.

The following table gives typical values for `$SECONDS`:

- Six months: 15778800
- One year: 31557600
- Four years: 126230400
- Eight years: 252460800

In our example, we will start a **1-year dissolve**, so we will use `Quill` to craft the following command:

**Inside air-gapped computer**

```bash
// Add the dissolve delay
$ quill --pem-file private.pem neuron-manage 5241875388871980017 --additional-dissolve-delay-seconds 31557600 > message.json

// Using "message.json", create QR codes you can scan with your phone
$ bash ./quill-qr.sh < message.json
```

Open file `message.png.`Send the message to the Internet Computer by scanning `message.png` with **`IC Transaction Scanner`** on your phone as in **2.2.**

![Screen Shot 2021-09-20 at 12.32.13 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5092c5cc-09d6-48e1-af0c-caa531ae0f56/Screen_Shot_2021-09-20_at_12.32.13_PM.png)

By now we should have the following:

[Outcome ](https://www.notion.so/c5520d4a64b24a3ca7c1650b79458f05)