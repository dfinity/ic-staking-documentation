---
layout: default
title: 4.0 Setting up your tools
parent: 4. Safest staking option
---

## 4.0 Getting your hardware and software  ready

What you will need:

- **air-gapped** computer (not connected to the internet)
- **networked** smartphone

You will need to install the following into your **air-gapped computer**:

1. [`Keysmith`](https://github.com/dfinity/keysmith) 
    - required to generate keys

2. [`OpenSSSL`](https://wiki.openssl.org/index.php/Binaries) 
    - required by `quill`

3. [`quill`](https://github.com/dfinity/quill)

4. [`qrencode`](https://github.com/fukuchi/libqrencode) 
    - Generates QR codes for bridging the air gap
    - `brew install qrencode`

5. [`jq`](https://github.com/stedolan/jq) 
    - Required for creating multiple QR codes
    - `brew install jq`

Because an **air-gapped computer** is not connected to the internet, it can be a bit awkward to install these. The most common way to do it is to download them to a **networked computer** and transfer the files to the **air-gapped computer** via CD or USB drive. Others install these on a networked computer *and then* air-gap it.
