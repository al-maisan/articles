# Introduction

The value of crypto-currency has gone up steeply making wallets increasingly the prime targets for cyber criminals. Now is the time to enhance the security of your crypto assets. This article shows how.

Unfortunately, all hardware and software has flaws meaning that any system can be broken and compromised. A time proven way to stay secure is *defense in depth* and compartmentalization i.e. securing your assets with multiple, independent controls that all need to be overcome by a potential attacker.

My objective was to set up a **single** Electrum wallet in such a way that two different hardware devices ([Ledger Nano S](https://www.ledgerwallet.com/products/ledger-nano-s) and [digital bitbox](https://digitalbitbox.com/)) are needed to sign *outgoing* bitcoin transactions.

This is slightly different from a classic multi-signature setup with multiple parties where e.g. 2 out of 3 wallets need to sign a transaction.

The setup presented here still has advantages over a wallet with `0` or `1` hardware devices:
* the actual private keys are never on the laptop i.e. even if your laptop is compromised the crypto assets are safe
* the setup uses 2 hardware devices of a different brand and make i.e. even if one hardware device is compromised the other will likely continue to protect the assets

For additional safety you can keep one or both hardware devices in a location that’s physically secured (e.g. a bank safe deposit box).

## Setup
* Laptop with [Fedora 27](https://getfedora.org/en/workstation/)
* Electrum-3.0.2
* Ledger Nano S
* Digital bitbox

## Assumptions
* you have a laptop with a fresh Fedora 27 install and `sudo` privileges
* Your user name on the laptop is: `user` (otherwise substitute accordingly in the instructions below)

## Overview

The steps are as follows:

1. install the additional software needed
1. prepare and set up the
   1. nano ledger
   1. digital bitbox
   1. electrum wallet

# Additional software

## Fedora packages
We will need a few packages that are not installed by default:
* `zbar-pygtk`
* `python3-btchip`
* `python3-protobuf`
* `python3-qt5`
* `compat-readline6`
* `bzip2-devel`

Please install these as follows

```bash
sudo dnf install -y zbar-pygtk python3-btchip python3-protobuf python3-qt5 compat-readline6 bzip2-devel
```

Then create a symbolic link that will be needed by the digital bitbox software later.

```bash
sudo ln -s `find /usr/lib64/ -type f -name "libbz2.so.1*"` /usr/lib64/libbz2.so.1.0
```

## Chrome web browser
Please install the chrome web browser [from here](https://www.google.com/chrome/browser/desktop/index.html) and Choose the `64 bit .rpm (For Fedora/openSUSE)` option. We will use the Chrome browser to run the Ledger Nano apps and test that the it is correctly recognized by our system.

# Nano Ledger setup

Please set up the device first ([instructions here](https://ledger.zendesk.com/hc/en-us/articles/115005161545-How-to-start-with-Ledger-Nano-S-)).


## Linux user name and group

The `id` command will tell you what your user name and group is, e.g. `foo` and `bar` in the example below.

```
$ id
uid=1000(foo) gid=1000(bar) groups=1000(bar),10(wheel) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

## Prepare the udev rules

Download [this file](https://drive.google.com/file/d/1Hj15PWBm8QrBZ9XrG1MzCMRB6lYGR4h9/view) with udev rules (SHA256: `f0d007ff0caaecd707f538b11266b8b2ef3436792902c53d394b71f7ed0940f6`) and make sure that the `GROUP` variable is set to your linux user group.

If your linux group is not `user` you will need to edit the downloaded file and replace all occurrences of `user` with your linux group name.

Once the file is ready, copy it to the appropriate directory and ask the system to load the new rules.

```bash
sudo cp <download path> /etc/udev/rules.d/20-ledger-nano.rules
sudo udevadm trigger
sudo udevadm control --reload-rules
```

## Chrome apps
Start the chrome browser and install these apps
* [Ledger Wallet Bitcoin](https://www.ledgerwallet.com/apps/bitcoin)
* [Ledger Manager](https://www.ledgerwallet.com/apps/manager)

Now insert the Ledger Nano, provide the PIN and make sure you can see it in the Ledger Manager app (the latter can be started from `chrome://apps/`). Also, make sure it has the latest firmware.

This is what you should see if it all works.

![This is what you should see](https://cryptostars.co/images/ledger-manager.png)


# digital bitbox setup


ownload the [file with the udev rules](https://drive.google.com/file/d/1YKRHfIRKuRY3oxT0TS1XoQuHGPfo-TeJ/view) (SHA256: `78db8717d95b078015cfd67acd94a148539e6ba65140dbcc644d6443e398c143`) and make sure the `GROUP` is set to your linux user group.

Once the file is ready, copy it to the appropriate directory and ask the system to load it.

```bash
sudo cp <download path> /etc/udev/rules.d/20-ledger-nano.rules
sudo udevadm trigger
sudo udevadm control --reload-rules
```

Download the [digital bitbox software](https://digitalbitbox.com/start_linux) and run it to [set up the device](https://digitalbitbox.com/start).

This is what you should see if it all works.

![This is what you should see](https://cryptostars.co/images/dbb.png)

## Electrum wallet software
* Download URL: https://download.electrum.org/3.0.2/Electrum-3.0.2.tar.gz
* SHA256: `4dff75bc5f496f03ad7acbe33f7cec301955ef592b0276f2c518e94e47284f53`

Unpack and run the Electrum wallet

```bash
mkdir -p ~/src; cd ~/src; tar xf <<download-path>>/Electrum-3.0.2.tar.gz; cd Electrum-3.0.2.tar.gz; ./electrum

```


## Udev configuration files
* Download URL: [digital bitbox](https://drive.google.com/file/d/1YKRHfIRKuRY3oxT0TS1XoQuHGPfo-TeJ/view)
* SHA256: 78db8717d95b078015cfd67acd94a148539e6ba65140dbcc644d6443e398c143


