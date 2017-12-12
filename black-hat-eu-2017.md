I had the opportunity to attend [Blackhat Europe 2017](https://www.blackhat.com/eu-17/) in London last week. What follows are some of my notes and observations.

*Nota bene*: this is all very subjective and not necessarily complete. You have been warned :-)

**tl;dr**
* many important breaches were known for months already e.g. the [Intel ME breach](https://twitter.com/_markel___/status/910567298083250182) or the [WPA2 Key Reinstallation Attack](https://arstechnica.com/information-technology/2017/10/severe-flaw-in-wpa2-protocol-leaves-wi-fi-traffic-open-to-eavesdropping/). However, the researchers presented the details in their talks and published papers and/or code immediately afterwards.
* most vulnerabilities are introduced by complexity and the need for backward compatibility
* attackers cause the most damage when they remain undetected after the compromise and can perform reconnaissance for months and years(!) - intrusion detection and incident response is key

# [Day 1](https://www.blackhat.com/eu-17/briefings/schedule/index.html#tab/wednesday)
## [Attacking nextgen roaming networks](https://www.blackhat.com/eu-17/briefings/schedule/index.html#attacking-nextgen-roaming-networks-8533)
Diameter, the successor to SS7, used in 4G/LTE mobile networks has all the same vulnerabilities *and* a new/unproven code base likely to contain additional bugs.

Take-away: telecom protocols tend to be super complex and have a *huge* attack surface.

[Slide deck](https://www.blackhat.com/docs/eu-17/materials/eu-17-Schmidt-Attacking-Next-Gen-Roaming-Networks.pdf)

In case you haven't heard of the SS7 attacks:
* [Real-World SS7 Attack — Hackers Are Stealing Money From Bank Accounts](https://thehackernews.com/2017/05/ss7-vulnerability-bank-hacking.html)
* [SS7 hack explained: what can you do about it?](https://www.theguardian.com/technology/2016/apr/19/ss7-hack-explained-mobile-phone-vulnerability-snooping-texts-calls)

## [Blueborne - a new class of airborne attacks that can remotely compromise any linux/iot device](https://www.blackhat.com/eu-17/briefings/schedule/#blueborne---a-new-class-of-airborne-attacks-that-can-remotely-compromise-any-linuxiot-device-8627)

First things first: turn off BlueTooth and leave it that way!

Bluetooth, again, is an old-school telecoms protocol, thus very complex and "sporting" a huge attack surface (the spec is 2822 pages long!)

Bluetooth stacks are big code bases that have received too little review and scrutiny due to lack of economic incentives. In hindsight, it is not surprising that almost all implementations are full of (security) bugs.

The BlueBorne attack vector can potentially affect all devices with Bluetooth capabilities, estimated at over 8.2 billion devices today.

[Slide deck](https://www.blackhat.com/docs/eu-17/materials/eu-17-Seri-BlueBorne-A-New-Class-Of-Airborne-Attacks-Compromising-Any-Bluetooth-Enabled-Linux-IoT-Device.pdf)

More info
* [Blueborne website](https://www.armis.com/blueborne/)
* [Bluetooth vulnerability can be exploited to silently hack phones and laptops](https://www.theverge.com/2017/9/12/16294904/bluetooth-hack-exploit-android-linux-blueborne)

## [Nation-state moneymule's hunting season – apt attacks targeting financial institutions](https://www.blackhat.com/eu-17/briefings/schedule/#nation-state-moneymules-hunting-season--apt-attacks-targeting-financial-institutions-8749)
It’s scary, banks are getting compromised all the time. Nation state actors used to be primarily after confidential information. However, analysis of attacks on South Korean banks (and bitcoin exchanges!) shows that these actors (North Korea in particular) are also getting into large-scale theft and bank robbery.
Attackers compromise financial organizations and then perform reconnaissance for months and years(!) before striking. Detecting intrusion / compromise and subsequent incident response is crucial to limiting damage.

[Slide deck](https://www.blackhat.com/docs/eu-17/materials/eu-17-Shen-Nation-State%20Moneymules-Hunting-Season-APT-Attacks-Targeting-Financial-Institutions.pdf)

## [How to hack a turned-off computer, or running unsigned code in intel management engine](https://www.blackhat.com/eu-17/briefings/schedule/#how-to-hack-a-turned-off-computer-or-running-unsigned-code-in-intel-management-engine-8668)

I never imagined intel would be this stupid / irresponsible; maybe there’s more behind this? Time for tinfoil hats?
* Intel’s ME can be hijacked
* full control of a machine, underneath and out of sight of whatever OS

[Slide deck](https://www.blackhat.com/docs/eu-17/materials/eu-17-Goryachy-How-To-Hack-A-Turned-Off-Computer-Or-Running-Unsigned-Code-In-Intel-Management-Engine.pdf)

[![Intel ME hack](https://cryptostars.co/images/jor.png)](https://twitter.com/rootkovska/status/938458875522666497)

* More coverage:
  * [Google Working To Remove MINIX-Based ME From Intel Platforms](http://www.tomshardware.com/news/google-removing-minix-management-engine-intel,35876.html)
  * [Intel's super-secret Management Engine firmware now glimpsed, fingered via USB](https://www.theregister.co.uk/2017/11/09/chipzilla_come_closer_closer_listen_dump_ime/)

# [Day 2](https://www.blackhat.com/eu-17/briefings/schedule/index.html#tab/thursday)
## [Security through distrusting](https://www.blackhat.com/eu-17/briefings/schedule/index.html#security-through-distrusting-9562)
In summary: everything humans produce is imperfect, don’t trust anything.
*  [Qubes OS](https://www.qubes-os.org/) runs on top of the XEN hypervisor
*  Every process runs in a separate VM
*  VMs are run in different contexts (e.g. work, personal etc.) and can be "single use" VMs e.g. for the browsing of untrusted web sites
*  Unless XEN is broken, the compromise in a particular VM / context is contained and does not infect the entire system
* more detail: [Rutkowska: Trust Makes Us Vulnerable](https://www.darkreading.com/vulnerabilities---threats/rutkowska-trust-makes-us-vulnerable/d/d-id/1330587)

[Slide deck](https://www.blackhat.com/docs/eu-17/materials/eu-17-Rutkowska-Security-Through-Distrusting.pdf)


## [Exfiltrating reconnaissance data from air-gapped ics/scada networks](https://www.blackhat.com/eu-17/briefings/schedule/#exfiltrating-reconnaissance-data-from-air-gapped-icsscada-networks-8662)

It is a miracle we don’t have *major* industrial control hazards / incidents on a daily basis
Major attack vectors:
* malicious USB
* infected external engineering laptop (used for maintenance)
* infected vendor updates

The researchers showed how to inject specially-crafted ladder logic code into Programmable Logic Controllers (PLCs). The hack generates encoded radio signals that can then be received by ordinary AM radios in order to exfiltrate sensitive data from air-gapped networks. 

[Slide deck](https://www.blackhat.com/docs/eu-17/materials/eu-17-Atch-Exfiltrating-Reconnaissance-Data-From-Air-Gapped-Ics-Scada-Networks.pdf)

[more detail](https://cyberx-labs.com/en/blog/cyberx-security-researchers-demonstrate-reconnaissance-data-exfiltration-air-gapped-ics-scada-networks/)
