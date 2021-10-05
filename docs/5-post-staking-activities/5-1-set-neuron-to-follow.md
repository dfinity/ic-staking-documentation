---
layout: default
title: 5.1 Voting or following with your neuron
parent: 5. Post-staking Activities
---
Warning: documentation in beta
{: .label .label-red }

* * *
# 5.1. Set your neuron to ***vote or follow***

*This step could happen many times per neuron.*

**Voting is critical** for staking because only neurons which vote receive rewards.

## 5.1.1 If you chose the **maximum ease staking option**... 

You should use the [NNS frontend dapp](https://nns.ic0.app/).

## 5.1.2 If you chose the **maximum control staking option**... 

Currently, voting is not possible with `quill`. 

- To vote you will have to do the following:
    1. Go to the NNS frontend dapp: [https://nns.ic0.app/](https://nns.ic0.app/)
        a. This may require you to get an [Internet Identity](https://identity.ic0.app/)
    2. Get your NNS frontend dapp principal for your identity anchor
    3. Add this principal as a Hot Key with `quill` to your neuron

        A hot key is a lot like a read-only view of a neuron, in that it lets you use a different controller to see the balance, maturity, dissolve delay, and other details of a neuron.

        Where this becomes most useful is in conjunction with the NNS frontend dapp and your Internet Identity. If you log in to the NNS App and visit the Neurons tab, it will display a Principal Id value at the top of that tab. Use that principal id with `quill` to establish the NNS App as a hot key for your neuron. We will use the following dummy principal: `2xt3l-tqk2i-fpygm-lseru-pvgek-t67vb-tu3ap-k0mnu-dr4hl-z3kpn-o2e`.

        Structure of command:
        ```bash
        $ target/release/quill --pem-file private.pem neuron-manage $NEURON_ID --add-hot-key $PRINCIPAL
        ```

        Command with example variables:
        ```bash
        $ target/release/quill --pem-file private.pem neuron-manage 5241875388871980017 --add-hot-key 2xt3l-tqk2i-fpygm-lseru-pvgek-t67vb-tu3ap-k0mnu-dr4hl-z3kpn-o2e

        // Using the bash script, create a QR code from the "message.json" file created by quill with your message
        $ bash ./quill-qr.sh < message.json
        ```

        Now refresh the NNS App in your browser, and you should see your Neuron displayed. You may change the followees and topics for the neuron now in the NNS App interface, but will not be able to dissolve, disburse or spawn.

        Open file `qr.png.`Send the message to the Internet Computer by scanning `qr.png` with your phone. This will navigate you `IC Transaction Scanner` on your phone as in 4.2.3.

        ![image](../assets/images/qr-code-scan-2.png)

    4. You can vote with that II via the NNS frontend dapp.
