---
layout: default
title: 4.0 Setting up your tools
parent: 4. Maximum Control Staking Option
---
Warning: documentation in beta
{: .label .label-red }

* * *
# 4.0 Getting your hardware and software ready

What you will need:

- **air-gapped** computer ([not connected to the internet](https://en.wikipedia.org/wiki/Air_gap_(networking)))
- **networked** smartphone

***
## Platforms supported

The scope and intent of this document is to support as many platforms as possible. 

Platforms: but the ones that have been most tested are:
* **Linux** - Very well tested
* **OSX (Intel)** - Very well tested
* **OSX (M1)** - Requires [Apple Rosetta](https://support.apple.com/en-us/HT211861), but very well tested
* **Windows** - Not very well tested yet.

If you experience any issues, please let us know via [issues](https://github.com/dfinity/ic-staking-documentation/issues) or make a [pull request](https://github.com/dfinity/ic-staking-documentation/pulls). These docs are for everyone in the Internet Computer community.

* * *
## Installing software

You will need to install the following into your **air-gapped computer**. 

Notet hat if you are using Ubuntu, you can install some of the necessary dependencies using the following command:
```
sudo apt-get install qrencode jq eog
```

1. `keysmith`
    - [https://github.com/dfinity/keysmith](https://github.com/dfinity/keysmith) 
    - You will use this generate important artifatcs like `seed phrase` and `private key`

2. `openssl`
    - [https://wiki.openssl.org/index.php/Binaries](https://wiki.openssl.org/index.php/Binaries)
    - Required by `quill`

3. `quill`
   - [https://github.com/dfinity/quill](https://github.com/dfinity/quill)
    - You will use this to craft messages like "create neuron" for the Internet Computer
    - You can install it by downloading the binary for your operating system; or by cloning and compiling the code (note that once compiled, the command to execute is `target/release/quill`) 

4. `qrencode`
    - [https://github.com/fukuchi/libqrencode](https://github.com/fukuchi/libqrencode) 
    - Generates QR codes for bridging the air gap
    - Tip: package managers make it easy to install, for instance if you have Homebrew, you can install via `brew install qrencode`

5. `jq`
    - [https://github.com/stedolan/jq](https://github.com/stedolan/jq) 
    - Required for creating multiple QR codes
    - Tip: package managers make it easy to install, for instance if you have Homebrew, you can install via `brew install jq`

6. Copy and paste the following bash script into a file named `quill-qr.sh`:

Warning: Only tested on MacOSX and Linux.

```bash
#!/usr/bin/env bash
URL=https://p5deo-6aaaa-aaaab-aaaxq-cai.raw.ic0.app
IFS=$'\n' read -r -d '' -a messages < <( cat - | jq -M 'if . | type != "array" then [.] else . end' | jq -rcM .[] && printf '\0' )

for message in "${messages[@]}"
do
    echo "$URL/?msg=$(echo "$message" | gzip -c | base64 | tr -d '\n' | sed -e 's/+/%2B/g' -e 's/\//%2F/g' -e 's/=/%3D/g')" | qrencode -t PNG -o qr.png
    if [[ ! -x /usr/bin/eog && ! -x /usr/bin/open ]]; then
        echo "To view QR codes on Linux, please install the 'eog' Gnome image viewer"
        exit 1
    else
        eog qr.png 2> /dev/null || open qr.png
        echo ENTER TO CONTINUE...
        read < /dev/tty
        clear
    fi
done
```

Because an **air-gapped computer** is not connected to the internet, it can be a bit awkward to install these. The most common way to do it is to download them to a **networked computer** and transfer the files to the **air-gapped computer** via CD or USB drive. Others install these on a networked computer *and then* air-gap it.

