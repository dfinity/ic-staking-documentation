---
layout: default
title: 5. Post-staking acivtivies
nav_order: 6
# has_children: true
permalink: docs/post-staking-activities
---
Warning: documentation in beta
{: .label .label-red }

# 5. Post-staking activitiess
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

# Post-Staking Activities

Congratulations, you have successfully staked ICP.

You can now do a few things:

## 5.1. Set your neuron to ***vote or follow***

*This step could happen many times 🔁 per neuron.*

**Voting is critical** for staking because only neurons which vote receive rewards.

a. If you chose the **easiest staking option**... go to the [NNS frontend dapp](https://nns.ic0.app/).

b. If you chose the **safest staking option**...

Currently, voting is not possible with `quill`. 

- To vote you will have to do the following:
    1. Go to the NNS frontend dapp: [https://nns.ic0.app/](https://nns.ic0.app/)
        1. This may require you to get an Internet Identity
    2. Get your NNS frontend dapp principal for your identity anchor
    3. Add this principal as a Hot Key with `quill` to your neuron

        A hot key is a lot like a read-only view of a neuron, in that it lets you use a different controller to see the balance, maturity, dissolve delay, and other details of a neuron.

        Where this becomes most useful is in conjunction with the NNS App and your Internet Identity. If you log in to the NNS App and visit the Neurons tab, it will display a Principal Id value at the top of that tab. Use that principal id with `quill` to establish the NNS App as a hot key for your neuron:

        ```bash
        $ quill --pem-file private.pem neuron-manage $NEURON_ID --add-hot-key $PRINCIPAL

        // Using "message.json", create QR codes you can scan with your phone
        $ bash ./quill-qr.sh < message.json
        ```

        Now refresh the NNS App in your browser, and you should see your Neuron displayed. You may change the followees and topics for the neuron now in the NNS App interface, but will not be able to dissolve, disburse or spawn.

        Scan the QR codes on the terminal to send the message to the Internet Computer with **`IC Transaction Scanner`** on your phone as in 2.2.

        ![image](../assets/images/qr-code-scan-2.png)

    4. You can vote with that II via the NNS frontend dapp.

## 5.2. Collect your neuron’s ***rewards***

*This step could happen many times 🔁 per neuron.*

a. If you chose the **easiest staking option**... go to the [NNS frontend dapp](https://nns.ic0.app/).

b. If you chose the **safest staking option**...

### 5.2.1 Command to “spawn rewards” from your neuron

If the dissolve delay of a neuron is equal to or greater than six months, it will accumulate voting rewards. This happens whether it is currently dissolving or not.

Once the amount of your reward is worth 1 ICP or more, you may spawn that "maturity" into a new neuron:

```bash
// This is just the structure, copy/pasting WILL NOT work. See below for working command
$ quill --pem-file private.pem neuron-manage $NEURON_ID --spawn$ quill ---pem-file private.pem neuron-manage 5241875388871980017 --spawn > message.json
```

```bash
$ quill ---pem-file private.pem neuron-manage 5241875388871980017 --spawn > message.json

// Using "message.json", create QR codes you can scan with your phone
$ bash ./quill-qr.sh < message.json
```

Scan the QR codes on the terminal to send the message to the Internet Computer with **`IC Transaction Scanner`** on your phone as in 2.2.

![image](../assets/images/qr-code-scan-2.png)

This command will display the neuron id of the newly created reward neuron. It will have a dissolve delay set to 7 days and be in a non-dissolving state, so you will need to use the `neuron-manage --start-dissolving` command above to begin dissolving that new neuron. In seven days you can then disburse it and the ICP will be transferred into the original controlling account.

### 5.2.2 Reward harvesting

a. If you chose the **easiest staking option**... go to the [NNS frontend dapp](https://nns.ic0.app/).

b. If you chose the **safest staking option**...

To sum up, once you've staked your ICP and created a neuron, the typical sequence of commands you will run, say monthly, to harvest rewards would be the following:

```bash
// This is just the structure, copy/pasting WILL NOT work.
$ quill --pem-file private.pem neuron-manage $NEURON_ID --spawn > message.json

// Using "message.json", create QR codes you can scan with your phone
$ bash ./quill-qr.sh < message.json
```

![image](../assets/images/qr-code-scan-2.png)


```bash
// This is just the structure, copy/pasting WILL NOT work.
$ quill --pem-file private.pem neuron-manage $REWARD_NEURON_ID --start-dissolving
// send message via QR codde app

// Using "message.json", create QR codes you can scan with your phone
$ bash ./quill-qr.sh < message.json

```

![image](../assets/images/qr-code-scan-2.png)


```bash

// 7 days later, disburse the neuron
$ quill --pem-file private.pem neuron-manage $REWARD_NEURON_ID --disburse
// send message via QR codde app

// Using "message.json", create QR codes you can scan with your phone
$ bash ./quill-qr.sh < message.json

```

![image](../assets/images/qr-code-scan-2.png)

**Note: The spawned neurons inherit your hotkeys**

## 5.3 ***Dissolve*** your neuron to get the ICP locked inside

*This step could happen many times 🔁 per neuron.*

a. If you chose the **easiest staking option**... go to the [NNS frontend dapp](https://nns.ic0.app/).

b. If you chose the **safest staking option**...

### 5.3.1 Command to start the dissolve process.

If you determine after some time that you wish to begin dissolving your neuron toward liquidation, you would use the `--start-dissolving` option of the `neuron-manage` command:

```bash
$ quill --pem-file private.pem neuron-manage $NEURON_ID --start-dissolving

// Using "message.json", create QR codes you can scan with your phone
$ bash ./quill-qr.sh < message.json 
```

![image](../assets/images/qr-code-scan-2.png)


### 5.3.2 Command to stop the dissolve process.

If you determine after some time that you wish to stop dissolving your neuron toward liquidation, you would use the `--stop-dissolving` option of the `neuron-manage` command:

```bash
$ quill --pem-file private.pem neuron-manage $NEURON_ID --stop-dissolving

// Using "message.json", create QR codes you can scan with your phone
$ bash ./quill-qr.sh < message.json 
```

![image](../assets/images/qr-code-scan-2.png)
