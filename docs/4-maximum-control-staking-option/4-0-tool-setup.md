---
layout: default
title: 4.0 Setting up your tools
parent: 4. Safest Staking Option
---
Warning: documentation in beta
{: .label .label-red }

* * *
# 4.0 Getting your hardware and software  ready

What you will need:

- **air-gapped** computer ([not connected to the internet](https://en.wikipedia.org/wiki/Air_gap_(networking)))
- **networked** smartphone

* * *
You will need to install the following into your **air-gapped computer**:

1. `keysmith`
    - [https://github.com/dfinity/keysmith)](https://github.com/dfinity/keysmith) 
    - required to generate keys

2. `openSSSL`
    - [https://wiki.openssl.org/index.php/Binaries](https://wiki.openssl.org/index.php/Binaries)
    - required by `quill`

3. `quill`
   - [https://github.com/dfinity/quill](https://github.com/dfinity/quill)
    - you will use this to craft messages like "create neuron" for the Internet Computer

4. `qrencode`(https://github.com/fukuchi/libqrencode) 
    - [https://github.com/fukuchi/libqrencode](https://github.com/fukuchi/libqrencode) 
    - Generates QR codes for bridging the air gap
    - Tip: if you have Homebrew, you can install via `brew install qrencode`

5. `jq`
    - [https://github.com/stedolan/jq](https://github.com/stedolan/jq) 
    - Required for creating multiple QR codes
    - Tip: if you have Homebrew, you can install via `brew install jq`

6. Copy and paste the following bash script into a file named `quill-qr.sh`:

```bash
#!/usr/bin/env bash
URL=https://p5deo-6aaaa-aaaab-aaaxq-cai.raw.ic0.app
IFS=$'\n' read -r -d '' -a messages < <( cat - | jq -M 'if . | type != "array" then [.] else . end' | jq -rcM .[] && printf '\0' )

for message in "${messages[@]}"
do
    echo "$URL/?msg=$(echo "$message" | gzip -c | base64 | tr -d '\n' | sed -e 's/+/%2B/g' -e 's/\//%2F/g' -e 's/=/%3D/g')" | qrencode > qr.png
    open qr.png
    echo ENTER TO CONTINUE...
    read < /dev/tty
    clear
done
```

Because an **air-gapped computer** is not connected to the internet, it can be a bit awkward to install these. The most common way to do it is to download them to a **networked computer** and transfer the files to the **air-gapped computer** via CD or USB drive. Others install these on a networked computer *and then* air-gap it.

