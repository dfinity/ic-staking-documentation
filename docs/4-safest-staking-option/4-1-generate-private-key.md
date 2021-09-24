---
layout: default
title: 4.1 Generate private key
parent: 4. Safest staking option
---


## 4.1 Generate a **private key**

*This step would only happen once 1️⃣ per cold wallet. For most people, this means you will do this step only once.*

Once you have `Keysmith` and `Quill` installed **air-gapped computer** ready, you are ready to start.

### 4.1.1 Use `Keysmith` to generate a seed text


Inside the **air-gapped computer**:
```bash
$ keysmith generate -o seed.txt
```

### 4.1.2 Use `Keysmith` to create a private key and store it in “*private.pem*” file


Inside the **air-gapped computer**:

```bash
$ keysmith private-key -o private.pem
```

### 4.1.3 Use `Keysmith` to display a `ledger account number`

This command will display a long string which is your `ledger account number`. Below, I provide an example of what this may look like.

Inside the **air-gapped computer**:

```bash
$ keysmith account
> 77b5eb9a465f4ce6f4da494ee2bfedeefe0b52d106e0272556c1ad991f99e3da 
```

You should write the `ledger account number` down.

### 4.1.4 Secure your `seed phrase` properly

Now that you have generated your `seed phrase` and your keys, you should write down the seed on paper or store it in some kind of steel wallet such as Bill Fodl.

To properly store your `seed phrase` see [where to store your seed phrase](../docs/safest-staking-option#1-where-to-store-your-seed-phrase)


***NOTE: Do not go to step 4.1.5 until you properly store it.***

### 4.1.5 Remove your `seed phrase` from your air-gapped computer

Now that the `seed phrase` is properly stored. You should delete it from your computer before moving forward so no one can use it to recreate your private key.  

Remove it with the following command:

Inside the **air-gapped computer**:

```bash
$ rm -vf seed.txt
```

### 4.1.6 Outcome

In this section, we did a few things, so let’s recap what we did and where we should be before moving forward.

**If you do not end up with a table that looks like the one below, do not continu**e. Try again, check out support, or submit a question to support.

| Artifact | Example1 | Security| Final outcome|
| :------------- | :------------- | :------------- | :------------- |
| `seed phrase` | `stove reject elder top dentist car suit license grid uncle ape wash`| • If someone has this, they can take your tokens. <br /> • If you lose it, you can lose access to your ICP. <br /> • You can keep this if you want to be able to generate your private key again. | • You created this via Keysmith in this section in 1.2.  <br />• You will have properly stored in 1.1<br />• You deleted this from your computer in 1.5|
| `private key` | ``| • If someone has this, they can take your tokens. <br /> • If you lose it, you can recreate from seed phrase <br /> | • You created this via Keysmith in this section in 1.2. |
| `ledger account number` | `77b5eb9a465f4ce6f4da494ee2bfedeefe0b52d106e0272556c1ad991f99e3da`| • If someone has this, they can view your token balance. <br /> • If you lose it, you can go through steps to get it back with your private key. | • You generate this in 1.3. This can be stored anywhere.


