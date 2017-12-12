# Introduction

The value of crypto-currency has gone up steeply making wallets increasingly the prime targets for cyber criminals. Now is the time to enhance the security of your crypto assets. This articles shows one way to do that.

Unfortunately, all hardware and software has flaws meaning that any system can be broken and compromised. A time proven way to stay secure is *defense in depth* and compartmentalization i.e. securing your assets with multiple, independent controls that all need to be overcome by a potential attacker.

This technique is implemented by setting up a **single** Electrum wallet in such a way that two different hardware devices ([Ledger Nano S](https://www.ledgerwallet.com/products/ledger-nano-s) and [digital bitbox](https://digitalbitbox.com/)) are needed to sign *outgoing* bitcoin transactions.

The setup presented here
* is slightly different from a classic multi-signature scheme with multiple parties where e.g. 2 out of 3 wallets need to sign a transaction.
* still has advantages over a wallet with `0` or `1` hardware devices:
  * the actual private keys are never on the laptop i.e. even if your laptop is compromised the crypto assets are safe
  * we use 2 hardware devices of a different brand and make i.e. even if one hardware device is compromised the other will likely continue to protect the assets

For additional safety, consider keeping one or both hardware devices in a location that’s physically secured (e.g. a bank safe deposit box).

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
1. Test it!

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

Please set up the device first as [described  here](https://ledger.zendesk.com/hc/en-us/articles/115005161545-How-to-start-with-Ledger-Nano-S-).


## Linux user name and group

The `id` command will tell you what your user name and group is, e.g. `foo` and `bar` in the example below.

```
$ id
uid=1000(foo) gid=1000(bar) groups=1000(bar),10(wheel) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

## Prepare the udev rules

Download [this file](https://drive.google.com/file/d/1Hj15PWBm8QrBZ9XrG1MzCMRB6lYGR4h9/view) with udev rules (SHA256: `f0d007ff0caaecd707f538b11266b8b2ef3436792902c53d394b71f7ed0940f6`) and make sure that the `GROUP` variable is set to your linux user group (edit the file and replace all occurrences of `user` with your linux group name if/as needed)

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

Last but not least install the Bitcoin wallet app on to your ledger nano device (by clicking the green circle with the little download arrow to the right of the Bitcoin symbol).

This is what you should see if it all works.

![nano ledger setup success](https://cryptostars.co/images/ledger-manager.png)


# digital bitbox setup


Download the [file with the udev rules](https://drive.google.com/file/d/1YKRHfIRKuRY3oxT0TS1XoQuHGPfo-TeJ/view) (SHA256: `78db8717d95b078015cfd67acd94a148539e6ba65140dbcc644d6443e398c143`) and make sure the `GROUP` is set to your linux user group.

Once the file is ready, copy it to the appropriate directory and ask the system to load it.

```bash
sudo cp <download path> /etc/udev/rules.d/20-ledger-nano.rules
sudo udevadm trigger
sudo udevadm control --reload-rules
```

Download the [digital bitbox software](https://digitalbitbox.com/start_linux) and run it to [set up the device](https://digitalbitbox.com/start).

This is what you should see if it all works.

![digital bitbox  setup success](https://cryptostars.co/images/dbb.png)

# Electrum wallet
* Download URL: https://download.electrum.org/3.0.2/Electrum-3.0.2.tar.gz
* SHA256: `4dff75bc5f496f03ad7acbe33f7cec301955ef592b0276f2c518e94e47284f53`

Insert and unlock the ledger nano and enter the Bitcoin wallet app (the little screen should read: "Use wallet to view accounts"). Also, insert the digital bitbox.

Unpack and run the Electrum wallet

```bash
mkdir -p ~/src/ ; cd ~/src/; tar xf ~/Downloads/Electrum-3.0.2.tar.gz; cd Electrum-3.0.2; ./electrum
```
  
You should see the Electrum install wizard now. Click next.

![Electrum install wizard, step 1](https://cryptostars.co/images/e-s1.png)

Supply a wallet name of your choosing or accept the default and click next.
![Electrum install wizard, step 2](https://cryptostars.co/images/e-s2.png)

Select the "Multi-signature wallet" type and click next.
![Electrum install wizard, step 3](https://cryptostars.co/images/e-s3.png)

Leave the "number of signatures needed" as is and click next.
![Electrum install wizard, step 4](https://cryptostars.co/images/e-s4.png)

Select the "Use a hardware device" option and click next.
![Electrum install wizard, step 5](https://cryptostars.co/images/e-s5.png)

On the "Hardware keystore" screen you should now see both devices. Click next.
![Electrum install wizard, step 6](https://cryptostars.co/images/e-s6.png)

When prompted, enter your digital bitbox password and click OK.
![Electrum install wizard, step 7](https://cryptostars.co/images/e-s7.png)

Use the digital bitbox seed by leaving everything as is and click next.
![Electrum install wizard, step 8](https://cryptostars.co/images/e-s8.png)

The public master key (of the digital bitbox) is displayed now. Just click next.
![Electrum install wizard, step 9](https://cryptostars.co/images/e-s9.png)

For the cosigner choose the "Cosign with hardware device" option and click next.
![Electrum install wizard, step a](https://cryptostars.co/images/e-sa.png)

Now select the nano ledger and click next.
![Electrum install wizard, step b](https://cryptostars.co/images/e-sb.png)

What you should see now is the following message: "Electrum is generating your addresses, please wait."

And, finally, the electrum wallet!
![Electrum install wizard, step c](https://cryptostars.co/images/e-sc.png)

The wallet screenshot above shows 2 test transactions I made to verify that all works. Yours will be empty.

# Troubleshooting

Make sure that the ledger nano is unlocked and runs the Bitcoin wallet app. It may [enter into stand-by mode](https://ledger.zendesk.com/hc/en-us/articles/115005161825-Auto-lock-mode) after a delay (10 minutes by default).

# Test it!

Do **not** start using the wallet for any serious amounts until and unless you have tested that it can receive *and* send bitcoin.
