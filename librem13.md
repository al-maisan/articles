I finally received my [Librem 13](https://puri.sm/products/librem-13/) laptop! What follows are my initial impressions. A more detailed article may follow after I have had the chance to use it for a longer period.

For the last couple of years I have been using a variety of Lenovo laptops (the T/X series and an X1 carbon more recently), so that's where my biases lie :-)

Why did I buy the librem? Mostly for the security / privacy features:
 * [hardware kill switches](https://puri.sm/learn/hardware-kill-switches/) for wlan / micro / web cam
 * [neutralized and disabled Intel ME](https://puri.sm/learn/intel-me/)

## tl;dr
In summary, the librem has a good, solid feel to it, nothing is twisting or creaking. The keyboard is very good and precise and the touchpad is fine as well. The machine is reasonably cool and gets a bit warmer on the bottom right-hand side (where the CPU sits?) when doing longish compile jobs for example. Also, the fan is fairly quiet and unobtrusive when it does kick in.

The display is nice and crisp and offers a lot of screen real estate (at a resolution of `1920 x 1080`). Having said that, I am not a very demanding user since I mostly process text one way or the other.

## Some highly subjective nit-picking
As I said already, the laptop is great. Most of my issues stem from the keyboard *layout*: particularly the
 * arrangement of the `Ctrl` and `Fn` keys being opposite from what I am used from the Lenovo keyboards (and no, the keys cannot be remapped in the BIOS)
 * absence of dedicated `Home`, `PgUp`, `PgDn` and `End` keys, meaning I have to press `Fn` in order to get these
 * `|` and `\` keys [do not work out of the box](https://forums.puri.sm/t/keyboard-layout-unable-to-recognize-pipe/2022/8)

The machine's design is best described by *elegant simplicity* and it's certainly a looker. On the flip side, when the lid is closed, there are no LEDs or other indications of the machine being suspended or the battery charging etc.

Last but not least [Qubes OS](https://www.qubes-os.org/) (`version 4`) does not install on the Librem 13 because [`VT-d` is not enabled in the BIOS (coreboot)](https://forums.puri.sm/t/vt-d-not-enabled-in-bios-coreboot/1225/8). I hope this last issue is fixed rather sooner than later since many "paranoid" types will want to run Qubes OS on their Librem :-)

![Qubes OS ver. 4 RC3 installer error](https://steemitimages.com/DQmP8BeemBWZFSBWZhHT2BMR5PuF3kquLQN9jRiMxYPTSws/qubes-installer-unsupported-hardware.png)

## Other reviews
 * [Purism Librem 13 v2 Linux laptop review](https://liliputing.com/2017/08/purism-librem-13-v2-linux-laptop-review.html)
 * [Review of the Librem 13 v2](https://medium.com/@christiankaindl/review-of-the-librem-13-v2-e637ab84e9af)
 * [Video: Purism Librem 13 v2 Linux laptop review](https://www.youtube.com/watch?v=PueUR_GpuuA)
