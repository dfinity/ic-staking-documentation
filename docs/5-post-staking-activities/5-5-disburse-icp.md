---
layout: default
title: 5.5 Disbursing ICP from a neuron
parent: 5. Post-staking Activities
---
Warning: documentation in beta
{: .label .label-red }

# 5.4  Disbursing ICP from a neuron

You can disburse the ICP from a neuron if any of the following are true:

a. Neuron was created without a dissolve delay

b. Neuron was created with dissolve delay, but it has dissolved longer than the dissolve delay.

You can now disburse the staked ICP in the neuron back into the main account it was staked from.

a. If you chose the **maximum ease staking option**...   you do not need this, you can already view it on the [NNS frontend dapp](https://nns.ic0.app/).

b. If you chose the **maximum control staking option**...

Structure of command:
```bash
$ target/release/quill --pem-file private.pem neuron-manage $NEURON_ID --disburse 
```

Command with example variables:
```bash
$ target/release/quill --pem-file private.pem neuron-manage 5241875388871980017 --disburse > message.json

// Using the bash script, create a QR code from the "message.json" file created by quill with your message
$ bash ./quill-qr.sh < message.json 
```

Note: this command typically requires only one QR code being sent.

![image](../assets/images/qr-code-scan-2.png)