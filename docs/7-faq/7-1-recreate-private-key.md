---
layout: default
title: 7.1 Recreate a private key
# has_children: true
parent: 7. FAQ
---
Warning: documentation in beta
{: .label .label-red }
    
# 7.1 How to recreate a private key
 
If you lose your privaye key you can recreate it so long as you still have your `seed phrase.`


## 7.1.1 place your `seed phrase` on your air-gapped computer

Retrieve your seed phrase from where you previously stored it and store it on your **air-gapped computer** in a file called `seed.txt`.

From a cryptography point of view, you technically only need the first four characters of every word in your seed phrases. That is why storage solutions like the Bill Fodl only store first four characters of every word.

To give a concrete example, supppose your `seed phrase` from `keysmith` was originally `wage roast present easy mobile olympic panda double ready unveil knock stage`. When you store it in Bill Fodl, you will actually only store the first four characters of each word like this: `wage roas pres easy mobi olym pand doub read unve knoc stag`.

In short, from a cryptography POV,

`wage roast present easy mobile olympic panda double ready unveil knock stage`

and

`wage roas pres easy mobi olym pand doub read unve knoc stag` 

will generate the same private key.

However, `keysmith` does not quite know that (at the time of this writing), so when using `keysmith` to recreate your `private key` you need to recreate the original `wage roast present easy mobile olympic panda double ready unveil knock stage` from the stored `wage roas pres easy mobi olym pand doub read unve knoc stag`. You can do that by using using this list of BIP-39 words: https://github.com/bitcoin/bips/blob/master/bip-0039/english.txt


## 7.1.2 Execute commands

Now that you have a `seed.txt` with the original `seed phrase`, you can run this command in the directory where `seed.txt` exists.

```bash
$ keysmith private-key -o private.pem
```

You will now have a file titled `private.pem` with your `private key`.

## 7.1.3 Secure your `seed phrase` properly

Now that you have generated your `private key`, you can leave it on your air-gapped computer. Make sure your `seed phrase` is properly sored for the future.

To properly store your `seed phrase` see [where to store your seed phrase](../docs/safest-staking-option#1-where-to-store-your-seed-phrase)

### 7.1.3 Make sure your seed phrase is properly stored

## 4.1.5 Remove your `seed phrase` from your air-gapped computer

Now that the `seed phrase` is properly stored. You should delete it from your computer before moving forward so no one can use it to recreate your private key.  

Remove it with the following command:

On the **air-gapped computer**:

```bash
$ rm -vf seed.txt
```