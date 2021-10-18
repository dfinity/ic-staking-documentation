---
layout: default
title: 4.3 Add more ICP to the Neuron
parent: 4. Maximum Control Staking Option
---
Warning: documentation in beta
{: .label .label-red }

* * *
## 4.3. *Optional*: Add more ICP to the Neuron (“top up the neuron”)

*This step could happen many times per neuron.*

Once you are confident your neuron is properly created, to “top up” an existing neuron, we will use the same command like the one in "4.2.2 Create a Neuron" (likely with a different `$AMOUNT` value), at any time.

Notes:

- It should print back to you the same Neuron ID as when you first staked it.
- In our example, we will send the neuron which we called “neuron3” the amount of 42.20 ICP.

**On the air-gapped computer**

```bash
//Craft message to send 42 ICP to the neuron named "neuron3". Store in "message.json"
$ target/release/quill --pem-file private.pem neuron-stake --name neuron3 --amount 42.20 > message.json

// Using the bash script, create a QR code from the "message.json" file created by quill with your message
$ bash ./quill-qr.sh < message.json
```

Open file `qr.png.`Send the message to the Internet Computer by scanning `qr.png` with your phone. This will navigate you `IC Transaction Scanner` on your phone as in 4.2.3.

![image](../assets/images/qr-code-scan-2.png)