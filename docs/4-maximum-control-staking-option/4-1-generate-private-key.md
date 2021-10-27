---
layout: default
title: 4.1 Generate private key
parent: 4. Maximum Control Staking Option
---
Warning: documentation in beta
{: .label .label-red }

* * *
# 4.1 Generate a **private key**

*This step would only happen once per cold wallet. For most people, this means you will do this step only once.*

Everything in this section occurs within your **air-gapped computer.**

<img src="../assets/images/air-gapped-computer.png" alt="drawing" width="300"/>

Once you have `keysmith` and `quill` installed **air-gapped computer** ready, you are ready to start.

* * *
## 4.1.1 Use `keysmith` to generate a seed text

On the **air-gapped computer**:
```bash
$ keysmith generate -o seed.txt
```

* * *
## 4.1.2 Use `keysmith` to create a private key and store it in `private.pem` file

On the **air-gapped computer**:

```bash
$ keysmith private-key -o private.pem
```

* * *
## 4.1.3 Use `keysmith` to display a `ledger account number`

This command will display a long string which is your `ledger account number`. Below, I provide an example of what this may look like.

On the **air-gapped computer**:

```bash
$ keysmith account
> 77b5eb9a465f4ce6f4da494ee2bfedeefe0b52d106e0272556c1ad991f99e3da 
```

You should write the `ledger account number` down or store it locally in a file so you can use in he next chapter in step **4.2.1.**. For moving forward, we will store it in a file called `account.txt`. Unlike `seed.txt` and `private.pem` the name can be anything.

* * *
## 4.1.4 Secure your `seed phrase` properly

Now that you have generated your `seed phrase` and your keys, you need to write down and store your seed phrase so that you could recover your private key in case you lost it.

To properly store your `seed phrase` see [where to store your seed phrase](../docs/4-maximum-control-staking-option#1-where-to-store-your-seed-phrase)


***NOTE: Do not go to step 4.1.5 until you properly store it.***

* * *
## 4.1.5 Keeping data on the air-gapped computer secret

Your air-gapped device should encrypt data and you must have a strong password. If this is not the case, an attacker who steals the device may get your private key. During occasional non-air-gap situations (which you should avoid if at all possible), e.g., you want to update one of the tools on the computer, you can delete the seed phrase and private key first, then after having re-entered air-gap mode retype the seed-phrase and recreate the private key. If you delete the seed phrase or the private key, be aware that default file removal often just removes the reference to the file on the computer without deleting the data. On MacOS you can use the '-P' flag to indicate both the file reference and the file data should be deleted and on Linux the 'shred' command can be used.

On an ***air-gapped computer** with MacOS you can for instance delete the seed phrase file and the seed phrase itself with the following command:

```bash
$ rm -Pvf seed.txt
``` 

* * *
## 4.1.6 Outcome

In this section, we did a few things, so let’s recap what we did and where we should be before moving forward.

**If you do not end up with a table that looks like the one below, do not continue**. Try again, check out support, or submit a question to support.

| Artifact | Example1 | Security| Final outcome| Storage |
| :------------- | :------------- | :------------- | :------------- | :------------- |
| `seed phrase` | `stove reject elder top dentist car suit license grid uncle ape wash`| • If someone has this, they can take your tokens. <br /> • If you lose it, you can lose access to your ICP. <br /> • You must store it in a safe and secure place in order to be able to regenerate your private key | • You created this via `keysmith` in this section in 4.1.1  <br />• You will have created and properly stored a backup in 4.1.4 | on paper or [Billfodl](https://privacypros.io/products/the-billfodl/), possibly kept in a safe |
| `private key` | ```-----BEGIN EC PARAMETERS----- ``` (and continues...) | • If someone has this, they can take your tokens. <br /> • If you lose it, you can recreate from seed phrase <br /> | • You created this via `keysmith` in this section in 4.1.2. | to remain on air-gapped computer |
| `ledger account number` | `77b5eb9a465f4ce6f4da494ee2bfedeefe0b52d106e0272556c1ad991f99e3da`| • If someone has this, they can view your token balance. <br /> • If you lose it, you can do step 4.1.3 to get it back with your private key. | • You generate this in 4.1.3. This can be stored anywhere. | wherever you like |

