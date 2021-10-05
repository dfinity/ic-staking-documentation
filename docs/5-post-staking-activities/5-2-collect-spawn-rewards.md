---
layout: default
title: 5.2 Collect neuron's rewards
parent: 5. Post-staking Activities
---
Warning: documentation in beta
{: .label .label-red }

# 5.2. Collect your neuron’s ***rewards***

*This step could happen many times per neuron.*

## 5.2.1 If you chose the **maximum ease staking option**... 

You should use the [NNS frontend dapp](https://nns.ic0.app/).

## 5.2.2 If you chose the **maximum control staking option**... 

If the dissolve delay of a neuron is equal to or greater than six months, it will accumulate voting rewards. This happens whether it is currently dissolving or not. Once the amount of your reward is worth 1 ICP or more, you may spawn that "maturity" into a new neuron.

Once you've staked your ICP and created a neuron, the typical sequence of commands you will run, say monthly, to harvest rewards would be the following:

1. Spawn rewards (which returns a new `neuron id` for the rewards)
2. Start dissolving the `neuron id` for the rewards
3. Wait 7 Days
4. Disburse the `neuron id` for the rewards. This gives you access to the ICP inside by placing it inside the `ledger account number` that created the original main neuron.

### 5.2.3 Spawn rewards” from your neuron

Structure of command:
```bash
$ target/release/quill --pem-file private.pem neuron-manage $NEURON_ID --spawn > message.json
```

Command with example variables:
```bash
$ target/release/quill ---pem-file private.pem neuron-manage 5241875388871980017 --spawn > message.json

// Using "message.json", create QR codes you can scan with your phone
$ bash ./quill-qr.sh < message.json
```

Open file `qr.png.`Send the message to the Internet Computer by scanning `qr.png` with your phone. This will navigate you `IC Transaction Scanner` on your phone as in 4.2.3.s

![image](../assets/images/qr-code-scan-2.png)

This command will display the neuron id of the newly created reward neuron. This new neuron will have a dissolve delay set to 7 days and be in a non-dissolving state, so you will need to use the `neuron-manage --start-dissolving` command above to begin dissolving that new neuron. In seven days you can then disburse it and the ICP will be transferred into the original controlling account. Be sure to store the `neuron id` of your newly created neuron from rewards so you can use it.

For our examples, we shall have the reward's neuron returned from 5.2.3 be `51111111199999999999`.

### 5.2.4 Start dissolving the neuron for the reward's neuron

To sum up, once you've staked your ICP and created a neuron, the typical sequence of commands you will run, say monthly, to harvest rewards would be the following:

Structure of command:
```bash
$ target/release/quill --pem-file private.pem neuron-manage $REWARD_NEURON_ID --start-dissolving
s```


```bash
// This is just the structure, copy/pasting WILL NOT work.
$ target/release/quill --pem-file private.pem neuron-manage 51111111199999999999 --start-dissolving
// send message via QR code app

// Using "message.json", create QR codes you can scan with your phone
$ bash ./quill-qr.sh < message.json

```

![image](../assets/images/qr-code-scan-2.png)


### 5.2.5 Disburse the reward's neuron

7 days after starting to dissolve your reward's neuron, you can disburse it which gives you access to the ICP inside. This will put the ICP into the original neuron's `ledger account number`. In our examples, this has been `77b5eb9a465f4ce6f4da494ee2bfedeefe0b52d106e0272556c1ad991f99e3da`.

```bash
// 7 days later, disburse the neuron
$ target/release/quill --pem-file private.pem neuron-manage 51111111199999999999 --disburse
// send message via QR code app

// Using "message.json", create QR codes you can scan with your phone
$ bash ./quill-qr.sh < message.json

```

![image](../assets/images/qr-code-scan-2.png)

Now you have the ICP from the rewards back in the `ledger account balance` that created your main neuron.

**Note: The spawned neurons inherit your hot keys**
