---
layout: default
title: 4.3 Add more ICP to the Neuron
parent: 4. Safest Staking Option
---

* * *
## 4.3. *Optional*: Add more ICP to the Neuron (“top up the neuron”)

*This step could happen many times 🔁 per neuron.*

Once you are confident your neuron is properly created, to “top up” an existing neuron, we will use the same command like the one in "4.2.2 Create a Neuron" (likely with a different `$AMOUNT` value), at any time.

Notes:

- It should print back to you the same Neuron ID as when you first staked it.
- In our example, we will send the neuron which we called “neuron2” the amount of 42.20 ICP.

**Inside air-gapped computer**

```bash
//Craft message to send 42 ICP to the neuron named "neuron3". Store in "message.json"
$ quill --pem-file private.pem neuron-stake --name neuron3 --amount 42.20 > message.json

// Using "message.json", create QR codes you can scan with your phone
$ bash ./quill-qr.sh < message.json
```

Scan the QR codes on the terminal to send the message to the Internet Computer with **`IC Transaction Scanner`** on your phone as in 2.2.

![image](../assets/images/qr-code-scan-2.png)