---
layout: default
title: 5.3 Start or stop dissolve process
parent: 5. Post-staking Activities
---
Warning: documentation in beta
{: .label .label-red }

# 5.3 Start or stop the dissolve process.

## 5.3.1 If you chose the **maximum ease staking option**... 

go to the [NNS frontend dapp](https://nns.ic0.app/).

## 5.3.2 If you chose the **maximum control staking option**... 

### 5.3.2 Command to START the dissolve process.

If you determine after some time that you wish to begin dissolving your neuron toward liquidation, you would use the `--start-dissolving` option of the `neuron-manage` command:

Structure of command:
```bash
$ target/release/quill --pem-file private.pem neuron-manage $NEURON_ID --start-dissolving
```

Command with example neuron:
```bash
$ target/release/quill --pem-file private.pem neuron-manage 5241875388871980017 --start-dissolving > message.json

// Using the bash script, create a QR code from the "message.json" file created by quill with your message
$ bash ./quill-qr.sh < message.json 
```

![image](../assets/images/qr-code-scan-2.png)

Note: this command typically requires only one QR code being sent.

* * *
### 5.3.2 Command to STOP the dissolve process.

If you determine after some time that you wish to stop dissolving your neuron toward liquidation, you would use the `--stop-dissolving` option of the `neuron-manage` command:

Structure of command:
```bash
$ target/release/quill --pem-file private.pem neuron-manage $NEURON_ID --stop-dissolving 
```

Command with example variables:
```bash
$ target/release/quill --pem-file private.pem neuron-manage 5241875388871980017 --stop-dissolving > message.json

// Using the bash script, create a QR code from the "message.json" file created by quill with your message
$ bash ./quill-qr.sh < message.json 
```

Note: this command typically requires only one QR code being sent.

![image](../assets/images/qr-code-scan-2.png)
