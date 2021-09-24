---
layout: default
title: 4.3 Add more ICP to the Neuron
parent: 4. Safest staking option
---

## 3. *Optional*: Add more ICP to the Neuron (“top up the neuron”)

*This step could happen many times 🔁 per neuron.*

Once you are confident your neuron is properly created, to “top up” an existing neuron, we will use the same command like the one in **2.1** Create a Neuron (likely with a different `$AMOUNT` value), at any time.

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

![Screen Shot 2021-09-20 at 12.32.13 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5092c5cc-09d6-48e1-af0c-caa531ae0f56/Screen_Shot_2021-09-20_at_12.32.13_PM.png)