---
layout: default
title: 4.2 Create neuron with dissolve delay (Part 3)
parent: 4. Safest Staking Option
---

{: .no_toc .text-delta }

1. TOC
{:toc}

* * *
# 4.2 Create a **neuron** with a **dissolve delay** 
## Part 3 of 3: Set dissolve delay

Now that you have a neuron, this section adds a dissolve delay to that neuron. Your ICP are not staked until the neuron has a dissolve delay.

* * *
## 4.2.5 Send a message to the neuron to “start dissolve delay”

To increase the dissolve delay of a neuron whose id is `$NEURON_ID`, we will use a command of the form:

```bash
// This is just the structure, copy/pasting WILL NOT work. See below for working command
$ quill --pem-file private.pem neuron-manage $NEURON_ID --additional-dissolve-delay-seconds $SECONDS
```

This shows the `neuron-manage` subcommand, which is used to manipulate neurons after they have been staked as in 4.2.2. In this case, we are adding `$SECONDS` seconds to the delay time.

The following table gives typical values for `$SECONDS`:

- Six months: 15768000 (60 seconds * 60 minutes * 24 hours * 182.5 days)   
- One year: 31536000 (60 seconds * 60 minutes * 24 hours * 365 days) 
- Four years: 126144000 (60 seconds * 60 minutes * 24 hours * 365 days * 4 years) 
- Eight years: 252288000 (60 seconds * 60 minutes * 24 hours * 365 days * 8 years) 

In our example, we will start a 1-year dissolve, so we will use `quill` to craft the following command:

**On the air-gapped computer**

```bash
// Add the dissolve delay
$ quill --pem-file private.pem neuron-manage 5241875388871980017 --additional-dissolve-delay-seconds 31536000 > message.json

// Using "message.json", create QR codes you can scan with your phone
$ bash ./quill-qr.sh < message.json
```

Open file `message.png.`Send the message to the Internet Computer by scanning `message.png` with `IC Transaction Scanner` on your phone as in 4.2.3.

![image](../assets/images/qr-code-scan-2.png)