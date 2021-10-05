---
layout: default
title: 7.2 Checklist for confidence
# has_children: true
parent: 7. FAQ
---
Warning: documentation in beta
{: .label .label-red }

# 7.2 Checklist for becoming confident with your tools

If you chose to custody your own neuron, tt is very important that you become familiar and confident with the self-custody staking process, because you are in full control of your ICP.

A common question is *"How can I become confident you would not mess things up?"* so this section has a simple checklist for testing and convince yourself that you both understand and installed everything correctly. If any step does not work or make sense to you, then you properly identified a gap in your tools or knowledge. That is ok! Identifying those gaps are the intent of this checklist.

## 1. Seed phrase and private keys setup

Goal: Show that you can generate the same private key from the same seed phrase and that you can recover the private key.

**1.1 [ ] Generate a `seed phrase` in `seed.txt`.**

```bash
$ keysmith generate -o seed.txt
```

**1.2 [ ] Generate a `private key` in `private.pem`.**

```bash
$ keysmith private-key -o private.pem
```

**1.3 [ ] Create a ledger account number and save it in `account.txt`**

```bash
$ keysmith account
```

**1.4 [ ] Store the `seed phrase` in 4-character words and delete `seed.txt` from your computer.**

a. [ ] Store your `seed phrase` offline

b. [ ] Delete the `seed phrase` from your computer

```bash
$ rm -vf seed.txt
```

**1.5 [ ] Rename `private.pm` as `private2.p2m`.**

```bash
$ mv private.pem private2.pem
```

**1.6 [ ] Rewrite the `seed phrase` into your computer in `seed.txt`.**

**1.7 [ ] Regenerate the private key in `private.pem`.**

**1.8 [ ] Compare `private.pem` and `private2.pem` to to make sure they are the exact same private key.**

```bash
$ diff private.pem private2.pem
```

if you got no differences, then you have  successfully moved your seed phrase, deleted it, stored it, and generated your private key when you needed it.

## 2. Create neuron with dissolve delay

Goal: Show that you can add, start, stop dissolve delays.

**2.1 [ ] Send at least 1.001 ICP to the ledger account number created in 1.3**

**2.2 [ ] Create a neuron**

a. [ ] Within air-gapped computer, craft a "create neuron" message with `quill` as in 4.2

b. [ ] Using a QR code, send the message to the Internet Computer as in 4.2

c. [ ] Verify that the neuron was created

**2.3 [ ] Add dissolve delay to the neuron**

a. [ ] Within air-gapped computer, craft a "add dissolve" message with `quill` 

b. [ ] Using a QR code, send the message to the Internet Computer

c. [ ] Verify that the dissolve was added

**2.4 [ ] Start the dissolve process**

a. [ ] Within air-gapped computer, craft a "start dissolve" message with `quill` 

b. [ ] Using a QR code, send the message to the Internet Computer

c. [ ] Verify that the neuron started to dissolve

**2.5 [ ] Stop the dissolve process**

a. [ ] Within air-gapped computer, craft a "stop dissolve" message with `quill` 

b. [ ] Using a QR code, send the message to the Internet Computer

c. [ ] Verify that the dissolve stopped

You have now been able to prove to yourself you can add, start, stop dissolve delays for your neuron. 

## 3. Add Hot key to NNS Frontend dapp

Goal: Add the NNS Fronted dapp as a "hot key" to your neuron so you can view it

3.1 [ ] Get the principal from the NNS frontend dapp

3.2 [ ] Within air-gapped computer, craft a "add hot key" message with `quill` as in 5.4

3.3 [ ] Using a QR code, send the message to the Internet Computer

3.4 [ ] Confirm you can view the neuron in the NNS Frontend dapp    
