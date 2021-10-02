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

A common question is *"How can I become confident you would not mess things up?"* so this section has a simple checklist for testing and convince yourself that you both understand and installled everything correctly. If any step does not work or make sense to you, then you properly identified a gap in your tools or knowledge. That is ok! Identifying those gaps are the intent of this checklist.s

## Seed phrase and private keys Setup

Goal: Show that you can generate the same private key from the same seed phrase

1. [ ] Generate a `seed phrase` in `seed.txt`.

```bash
$ keysmith generate -o seed.txt
```

2. [ ] Generate a `private key` in `private.pem`.

```bash
$ keysmith private-key -o private.pem
```

3. [ ] Store the `seed phrase` in 4-character words and delete `seed.txt` from your computer.

a. Store your `seed phrase`

b. Delete the `seed phrase`

```bash
$ rm seed.txt
```

4. [ ] Rename `private.pm` as `private2.p2m`.

```bash
$ mv private.pem private2.pem
```

5. [ ] Rewrite the `seed phrase` into your computer in `seed.txt`.

6. [ ] Regenerate the private key in `private.pem`.

7. [ ] Compare `private.pem` and `private2.pem` to to make sure they are the exact same private key.

```bash
$ diff private.pem private2.pem
```

if you got no differences, then you have  successfully moved your seed phrase, deleted it, stored it, and generated your private key when you needed it.
