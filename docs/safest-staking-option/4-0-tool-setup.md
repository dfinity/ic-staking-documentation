---
layout: default
title: 4.0 Setting up your tools
parent: 4. Safest staking option
---

## 0. Getting your tools ready

What you will need:

- **Air gapped** computer (not connected to the internet)
- **networked** smartphone

You will need to install the following into your **Air gapped computer**:

- [`Keysmith`](https://github.com/dfinity/keysmith)
    - Installing Keysmith
        1. Download the tarball
            1. Mac: darwin-amd64
                1. you may need to "download saved file as .gz"
            2. Linux: 
        2. Follow install steps
- `[OpenSSSL](https://wiki.openssl.org/index.php/Binaries)` - Required by `quill`
    - Installing Open SSL
        - may require `homebrew`
- [`Quill`](https://github.com/dfinity/quill)
    - installing Quill
        1. Download
            1. Mac: 
        2. Will re
- `qrencode` - Generates QR codes for bridging the air gap
    - `brew install qrencode`
- `jq` - Required for creating multiple QR codes
    - `brew install jq`

Because the **air-gapped computer** is not connected to the internet, it can be a bit awkward installing these. The most common way to do it is to download them to a **networked computer** and transfer the files to the **air-gapped computer** via CD or USB drive. Others install these on a networked computer *and then* air gap it.