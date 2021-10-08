---
layout: default
title: 6.1 Raspberry Pi
# has_children: true
parent: 6. Alternative Staking Options
---
Warning: documentation in beta
{: .label .label-red }
    
# [Experimental] Self-custody with Raspberry Pi Zero

This document is an experience report on using Raspberry Pi Zero and `ic-repl` as the self custody solution for managing ledger accounts and neurons.

***
## Why Raspberry Pi Zero

It’s a very good air gap machine: It has no wifi, no bluetooth, and no speaker. Even if your air gap machine is compromised, it is physically not possible to transfer the private key out.

Financially, it costs only 5 dollars! You may need to buy some adapters, but the total cost should be less than $30, assuming you already have a monitor or TV.

Here is a list of hardware that is needed for the air gap setup:
* Raspberry Pi Zero (Don’t buy the Zero W version, which includes the Wifi chip)
* Micro-USB power adapter (5V, 2.5A)
* Class 10 microSD card
* Mini-HDMI to HDMI adapter
* HDMI monitor or TV
* Micro-USB to USB OTG hub
* USB keyboard
* USB stick
* (Optional) A case for Pi Zero

***
## Why ic-repl

[ic-repl](https://github.com/chenyan2002/ic-repl) is a generic tool for communicating with canisters with Candid. It has an offline mode, where canister calls become signed messages embedded in the QR codes. You can then use your smartphone’s camera to send the message to the IC.

Compared with quill, there are several advantages:
* `ic-repl` is an interpreter for Candid, which means the binary rarely needs to be upgraded. The fewer we upgrade, the safer the air-gap machine.
* Every command in quill is a canister call. If we want to add a new command or change an existing command’s arguments, we need a new binary release. In `ic-repl`, all canister calls are written in a textual script, which can be extended without new binary release. It also adds more transparency, so that users know exactly what calls are executed for each command.
* Quill outputs the json message, which can be converted to QR code with external tools. `ic-repl` generates QR code natively without relying on external tools.

Overall, both quill and `ic-repl` depend on the same set of crates, for example, ic-agent, candid, ledger canister and openssl. If you just want to self-custody your neurons, you can use either. If you want to perform more operations, such as voting, from the air gap machine, you need to use `ic-repl`.

***
## Installation

To boot the Raspberry Pi, we need to image the microSD card with Raspbian OS with [Raspberry Pi Imager](https://www.raspberrypi.com/software/). The default OS contains XWindows, which is not needed for our setup. We can choose the Lite version, which is terminal only and much smaller than the default image.

### OS Setup

The default login user is "pi" and the password is "raspberry". Remember to change the default password. The default keyboard layout and timezone is UK. To change the locale, run
```bash
$ sudo raspi-config
```
And select "Localisation options"/"Timezone" and "Keyboard".

### Install packages

There are three software packages we want to install:

1. Disk encryption tool: `ecryptfs`. 
   It is recommended to encrypt at least the home directory, where you store the private key. This ensures that if the SD card is stolen, people cannot access your private key. There is a small chance that the private key can leak outside of your encrypted directory, for example in the swap space. A more secure method is to encrypt the whole SD card, but it is an involved process for Raspberry Pi. Interested readers can refer to [this article](https://rr-developer.github.io/LUKS-on-Raspberry-Pi/) for more information.
   
2. Framebuffer viewer: `fbi`. 
   `ic-repl` generates QR code either as ascii characters or as png images. Ascii characters are more convenient to use, but if the message is large, it may not fit in one screen. In that case, you need to use the png image. Since we didn’t install XWindows, we need an image viewer that works in the terminal.
   
3. Tools for key generation and signing messages: [keysmith](https://github.com/dfinity/keysmith/releases), [ic-repl](https://github.com/chenyan2002/ic-repl/releases) and [quill](https://github.com/dfinity/quill/releases) (quill is not strictly necessary, but it doesn’t hurt to have both).

I have collected all the binaries in a git repository ([https://github.com/chenyan2002/pi-wallet/](https://github.com/chenyan2002/pi-wallet/)). To install the first two packages, you can copy all the deb files into your USB stick, and copy to your Raspberry Pi. To mount the USB stick and install the packages,

```bash
$ sudo mount -t vfat /dev/sda1 /mnt/usb
$ cp /mnt/usb/deb/*.deb <home_directory>
$ sudo dpkg -i *.deb
```

If you want to reproduce the deb files from the [raspbian repository](https://archive.raspbian.org/raspbian/pool/main/), you can run the following command to get all the necessary dependencies,
```bash
$ sudo apt-get install --print-uris fbi ecryptfs-utils lsof cryptsetup
```

### Encrypt home directory

It is recommended to encrypt at least the home directory, where you store the private key. This ensures that if the SD card is stolen, people cannot access your private key. 

```bash
$ sudo modprobe ecryptfs
$ sudo adduser <username>
$ sudo usermod -a -G video <username>  // Enable fbi
$ sudo usermod -a -G sudo <username>  // Need to run “sudo date -s”
$ sudo ecryptfs-migrate-home-u <username>  // Encrypt user’s home dir
$ // make sure you can login with <username>
$ sudo swapoff -a -v   // Disable swap space to prevent data leak
$ sudo systemctl disable dphys-swapfile.service
$ sudo reboot
$ free  // make sure swap space is 0
```

For a more detailed explanation, refer to [this tutorial](https://technicalustad.com/how-to-encrypt-raspberry-pi-home-folder/).

***
## Generate seed and private key

Remember to perform the following commands in your encrypted directory:

1. Generate seed if you don’t have one:
```bash
$ keysmith generate -o seed.txt
```
2. Generate `private.pem`:
```bash
$ keysmith private-key -o private.pem
```
3. Write down the seed on paper.
4. Permanently remove `seed.txt`.
```bash
$ shred -v -n 1 seed.txt  // Overwrite with random data
$ sync  // forcing a sync to disk (small file I/O in ext4 can buffer)
$ shred -vfzu -n 5 seed.txt
```

***
## Using ic-repl

Each time you reboot the Raspberry Pi, you need to manually synchronize the time, since the machine is offline.

```bash
$ sudo date -s "YYYY-MM-DD HH:MM:SS"
```

It is important to make the time reasonably accurate, because the signed message has an expiration time of 5 minutes based on the system time.

After generating the private key with keysmith, we can use `ic-repl` to sign the message and use your smartphone to send the message. The command can either be stored in a script file, or run interactively in the REPL environment. Here is an example run of `ic-repl` in offline mode. You can refer to the [grammar for ic-repl](https://github.com/chenyan2002/ic-repl#commands) for more commands.

```
$ ./ic-repl --offline
Canister REPL
anon@ic 1> identity private "./private.pem"  // import private identity
Current identity xxxxx-xxxxx-xxx
private@ic 2> account(private) // compute account id from private
“xxxxxxxxxxxxxxx”
private@ic 3> call ledger.account_balance_dfx(record { account = account(private) })  // check for account balance
```
<pre style="line-height: 1; font-size: 8pt">
    █▀▀▀▀▀█     ██▀▀█▀  ▀▄▀▀▀█ █▄▀▀██ █▄▄▀   █▀▄ █▀  ▀   ███▄ █ ▀ ▀▄ ▄▄ ▄ █▀▀▀▀▀█
    █ ███ █   ▀█▀▄█▄▄▄▀█ ▄ ▄█ ▀▀▀▀▄▀ █▄ ▀  ▀▀▀▀ ▀█ ▀▄ ▄▄▄█▀▄   ▄▀▄█▄▄█  █ █ ███ █
    █ ▀▀▀ █ ▄▀▄▄ ▀▀▄▄▀▄   ▀██▀▀▀██▀▄▀█▀▄▄█▀  ▀▀▄█▀█▀▀▀█▀▄▄▄▀ ▄█▀▀█▀█▄▀█▀▀ █ ▀▀▀ █
    ▀▀▀▀▀▀▀ ▀ ▀▄▀ ▀ ▀ █ █ █▄█ ▀ █▄█▄▀ ▀ ▀▄▀ █ █ ▀ █ ▀ █▄▀▄▀ ▀ █▄█▄█ ▀ █▄█ ▀▀▀▀▀▀▀
    ▀▄▄█▄█▀▄█ █▄▀▄▀ ▄▀▀█▀ ▀██▀█▀▀▀▄▄  ▄▀▀▀▀█▄ ███ ▀██▀█▄▀██▄▀█  █▀ ▄▄▄ ▄██▄█▄▄▄
    ▀▄██▀▀▀█▄▄ ▄▄█▄ ▀██▀ ▄▀  █▄█▀▄█▄ ▄▄█ █▀▄▀ █ ▄▄█▀▀▀ █ ▄ ▄  ▀▀ █▀▀▄▄▄█▄  █▀▄ █▄
     ▄ ▀▄▄▀▀▄  ▀▄   ▄▄  ▀▀ █ █  ▀ ▄█▀███▀▄▀█▀ ▄▀ █▀▄▄█  █▄█ ▄▀▀▄█▀█▄▄ ▄▄ ▀▄ ▄█▀ ▄
    █  ▄▀▄▀ ██▄ █▀██ ██ ▀▄▀▄ █▀▀▄▀█ █▄▄▀ █ ▀▀ ██▀▄▀▄█▄▀▄█ █▄▄ ▄▄ ▄▄▄███▀   ▀▀▄█▀
    ▄ █ ██▀▄▀▀▀ ██▄▄▀█▀▀▀█ ▀ █ █▀▄▄██▄▀▄▀ ▀▄█ ▀█▄▄▄▀▄█▀█▄███▄  ▄▀▀▀▀▄ ██▀██▄▀▄█▀▀
    █ ▄███▀▀▀▄▀▀▄▀▀▄ █▀██  ▄███   ▀▄▄▀ ▄▄ ▀▀█ ▀█ ▄▀▄▄█ ▄▀▄▀ ▄ ▄██ ██▄ █ ▄█▄▀█▀▀▄█
    ▀██▀▄ ▀▀▀▀█▄ ▄██ ▄█▀█▄██▄ ██ ▄█▀ ▀  ▀▀▀▀▄ ▀█▀▄█▄█▄  █▄█▀▀▄▄ ▀ ▄ ▀▄▀█ █▀  ▀▄██
    █▄ ▀█▄▀▄▀ ▀▄▀ ▄ ▀▀▄▄██▄▄▄██▀█▀▀▀██▄▄▄▀█▀ █████▀ ▄ ▄▄█▄█▄▄▄▀  █▄██▀▀▄ ▀▄ ▀▀█▀
    ▀▀▀▀█▀▀▀█ ▀█▄▄▄ ▀██▄▄▄▀▄█▀▀▀█ ▄▄▀▄▀▀▀█▀▀ █▀█▄▄█▀▀▀█▄▄▄▄▀ ▀█▄  ██▀▄▀██▀▀▀█ ▄ █
    ▄ ▀▀█ ▀ █▄▄ ▄▀█▀ ▄▀▄█▄█ █ ▀ █ █  ▄▀██▀▄▄█▄█  ██ ▀ █▀██▄▀▄ ▄▄▄ ▄█ ▄▀▄█ ▀ █▀ ▀▀
     ▄  █▀▀█▀▄▄▀▀▄█▄█ ▀▄█ ▀ ▀██▀▀▄▀▀█▄▀█▀██▀   ▀██▀▀▀█▀▄█▄██▀▄▀ ▀██▄▄ ███▀█▀▀▀▄▄█
    █ ▄▄▄▄▀ █▄▄ ██▀▄ █  ▄ ▀█▀█▄▀ █▀▄▀██ ▀▀█▀▀█▀  ▄██▄ ▄█▄▄▄ █▄ ▄▀▀ █ ▄ ▀  ▄▄▀█ █▀
     ▀▀█▀▄▀ ▀▀▀█▄██▄ ▄██▀▄▀ █▀▄█▀▄▀▄▀▀ ▀▀▀▀ █▄▀█▀███▀██▄ ▀█▄▀▄██ █▄▀▄█▀█▀ ▄▄█  ▀▄
    █▄ ▄██▀▀▄ ▀▄█▀  ▄▀▀▀ ▄ ▀▄▀▀ ▀▀▀▄██  ▀▄██▄▀▀▄▄▀ ▄ ▄ ▄█ ▄ ▀ ▄ █▄▄▄▀██▀▀▀  ▄ ██
    ▀▄█  ▀▀▀▄█▀▄ ▄█▀▀█▄ ▄▀▀▀▄  ▄▀█▀▄▀ ▄▄▀▄▀██▀▀▀█ ▄▀▄▀▄█▀ ▄  ▄ ▄▄ ██▀▄▄▄▄▀▄▄▀▀▄▄█
     ▄ ▀▀▄▀█▀▀▄   █▀ ▄▄█▀ ▄██▀▄▄▄▄█ ▀█▀▀▀█ ▀▀▀▄ ▀▄▄▀▄██▄ ███▀█ ▄██▄█ ▀█ ▄▄█▀█▄▄█▄
     █▄█▄█▀▄▄▀▄▀█ ▀██  ▄   ▀▄▄███▄  ▄█▀▄█▄█  █  █▀ ▀ ▀▄▀▄ ██▄▄▀ ▄▀ █▀ █▄██▄▀▀▄█▀▀
    █▀▄ ▀█▀ ▄   ▄▀▀▄ █  ▄█  ▄██▀ ▀▄▄▀██▄ ██ █▀▀▄█▀▄ █ ▄▄▄▄█  █ ▀ ▄█▀▀▄█▀█▄▀▀▀▀  █
    ▄▄█ ██▀▀██▄  █▀▄▀▄█▄▄▄▄▄▀▄▀ ▄▄ ▄▄█▀ ▄▀ █▀█▀▀   ▄▀ ▀█▄██▄▄▄ █▀█▀▄█ ▀▄▄▀█▀▀█▄ ▀
     ▀▄▀█▀▀▀█▄█▀▄█▀▀███▀█ █▀█▀▀▀█▀  ▄█   ▀▄  █▄ ▄██▀▀▀█▄▀█ ▄▄ ▀▀ █  ▄ █▄█▀▀▀█ ▀█▀
    ▀ ▄ █ ▀ █▄███ ██ ▄▄▀▄▄█ █ ▀ █▄ █▀████▄▀ █▀█▄▀ █ ▀ █ ▄██▄▀  ▄ █▀  ▄█ █ ▀ █▀▀ ▄
    ▀█ ▀█▀▀▀█ ▀▀▀ ▄▄██  ▀▀█▀██▀▀██  ▄▀█▀▀  ▀ ▄▀▄ █▀█▀▀██ █▄██ ███▄▄▀▄▀███▀▀█▀▀▀▀▄
    ▄▀▄▄▄▄▀█  █▄ ▀▄ ▄▄██  ▄▄▄▄▀███▄█▀ ▀ ▀ ▄▄▀▀██▄▀▀▀▀▀▀    ▀▄▄▄ ██▀ ████ ▀ ▄▀▄█▄
    ▀▄█▄▀▀▀█▀▄▀  ██▄▀▄▄▄██ ▀▀▀▀▄ █▄▄█▀▄▀ ▄▄▀▄ ██▀▄██ ▄▄█ ▀█▀▄ ▀▄  ▄█▄ █ ▀ ▄ ▄▄▄▄█
    ▀█▄▄▄ ▀█▄█ █▄ ▀██▀▄▄█ ▄▀▀ ▄▄ ▀█  ▀ █▀█▄▄▄█  ██▄▄█ ▄▄ ▄█ ▀█ █ ▀█▄   ▄▀▀▀ ▀ ▄▀▀
      ██▀ ▀▄▀█ ▄  █▄▀█▀█▀   █ ▀▄▄▀ █  ▀█▀ ▀ ▀▀▀▀█▄▄▀▄▀▀▄▄▄▄▄   ▀▄▀ ▄█▄ █  █ ▄▀ ▄▀
    ▄  █▀ ▀ ▀   ▄▄▀▄ ▀▀▀██▄ ▀ ▀▄ █▀▀█▀█▀▀▀█▄▀ ▄▄ ▀ ▀▀ █▄▄  ▄▀▄▄▄█  █▀█▄▄█▀▄██ █
    ███ ▄█▀ ▀█▀▄▄▄▀    ▀▀▀ ▄▄▀█████▄ ▀▄█▀▀▄▀ ██  ██▄▀▄▄█▄▀▄█▀▄▀█  █▄█ ▀▄▄ ▄█▄  █▀
    ▀█▄▄ ▀▀  ▄▄▀▄▀█▄ ▀▄ ▀▄▀  ▄▀█▄ ▄▄   █▀▄▀█ ▄▀▀█   ██▀▄▀█▀█▀ ▀▀▄ ▄ ▀▀▄ ▀ ▀██▄▄ █
     ▀  █▀▀█▄██▄█▄   █▄ █▄▀█▄▄▀█▄██▀ █▀█▄▀█ ▄▄█▄▀ █▀▀ █▀█ ▄▄▄ ▀▄ ▄ █▄▀█ ▀ █▀ ▀ ▄█
     ▀▀▀▀ ▀▀▄  █▀▀ █ █▄▄██▄▀█▀▀▀█▄ ██▀  █ ▄▀█▀▀█▄▄█▀▀▀█▄ ▀█▄▀▄▀▄▄▄█▀▀█▄▀█▀▀▀███▄▄
    █▀▀▀▀▀█ ▄ ▀███▄ ▄▄██▄▄▀ █ ▀ █▄  ▄█  ▀ █▀ ██▄▄▄█ ▀ █▄▄ ▄▄▀ █▀ ▄▄█▀██ █ ▀ █▀▄ ▄
    █ ███ █ ▄  ▄▀██▄█ ▄▀ ▄▄▀▀█▀▀█ ▀▄▄ ██▄▀█▀█ ▄ ▄███▀██▀▀▀▀▄ ▀▄▀█▀▄█▀█▀▄▀██▀▀█▀██
    █ ▀▀▀ █  ▀▄ ▄█▀▄▄▀█▄▀█ ███▄  ▄▄  █▀▄ █  █▀▀▀▀█▄█▀█▄█▄▀█ ▄  ▄██▄▄ ▀▄ ▄█▀ ▀▄ ▄▀
    ▀▀▀▀▀▀▀ ▀▀ ▀   ▀ ▀ ▀ ▀  ▀   ▀▀  ▀  ▀▀▀▀▀  ▀ ▀▀   ▀ ▀▀▀▀▀▀▀▀ ▀ ▀▀    ▀     ▀▀
</pre>

By default, each call generates a QR code in ascii characters, so that it can be displayed in the terminal directly. Both iOS and Android have native support for QR code, so you can use your smartphone’s camera app to scan the QR code, and a browser URL should pop-up, which directs you to Paul Liu’s [ic-qr-scanner canister](https://github.com/ninegua/ic-qr-scanner) to send the signed message.

You can also store the commands in a script file, and run the script in the terminal. For example, [https://github.com/chenyan2002/pi-wallet](https://github.com/chenyan2002/pi-wallet) lists the script files to stake, config neurons. You can run the script via,

```bash
$ ./ic-repl --offline stake.sh
```
or
```bash
$ ./stake.sh
```

Depending on your monitor’s resolution, you may notice that the ascii QR code is sometimes too large to fit in one screen, so that we cannot scan them. In this case, you will need to generate a png file for each call. You can do this via,

```bash
$ ./ic-repl --offline --format png stake.sh
$ fbi msg1.png  // view the first QR code
$ fbi msg2.png  // view the second QR code
```

### Message size limit

There are size limits to the QR code approach.
* QR code can hold about 4000 characters
* The encoded URL can be at most 2000 characters

Luckily, most calls to NNS and ledger canisters are less than 2000 characters. The largest I have seen so far is around 1800 characters. 

If we want to go beyond the 2000-character limit, we can use --format png_no_url or --format ascii_no_url flag to generate QR code which embeds only the signed message without the URL. To scan this QR code, you will need to go directly to the ic-qr-scanner canister, and use the scanner there.
