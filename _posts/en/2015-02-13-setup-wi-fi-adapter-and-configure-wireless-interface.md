---
lang: en
ref: setup-wi-fi-adapter-and-configure-wireless-interface
title: Setup Wi-Fi Adapter and Configure Wireless Interface
date: 2015-02-13T10:57:11+00:00
author: Arthur Gareginyan
layout: post
permalink: /linux/setup-wi-fi-adapter-and-configure-wireless-interface.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - adapter
  - asus
  - connect
  - dongle
  - firmware-realtek
  - n-10 nano
  - wi-fi
  - wifi
  - wpasupplicant

---

![thumb](/images/Wi-Fi-ASUS-N-10-Nano.png)
I'll show an example of how to configure a connection to a wireless network from the console of the Debian system by using Wi-Fi Adapter “ASUS USB-N10 Nano” (`ID: 0b05:17ba`, `Driver: rtl8192cu`).


### Installing driver/firmware for Wi-Fi Adapter

Wi-Fi Adapter “ASUS USB-N10 Nano” is uses the driver "rtl8192cu", wich can be found in the `firmware-realtek` package.

**1.** Add a `non-free` component to `/etc/apt/sources.list`, for example:

<pre>
# Debian 7 "Wheezy"
deb http://http.debian.net/debian/ wheezy main contrib non-free
</pre>

**2.** Update the list of available packages and install the `firmware-realtek` package:

```
sudo apt-get update
sudo apt-get install firmware-realtek
```

**3.** Connect the device to your system.

Now the adapter is setuped.


### Scaning Networks

Scan for available networks and get network details:

```
sudo iwlist scan
```


### Configure Wireless Interface

**1.** We are going to connect to the wireless network with WPA-PSK/WPA2-PSK authentication method, so before continuing, we need to install the `wpasupplicant` package:

```
sudo apt-get install wpasupplicant
```

**2.** Restrict the permissions of `/etc/network/interfaces`, to prevent pre-shared key (PSK) disclosure:

```
sudo chmod 0600 /etc/network/interfaces
```

**3.** Open `/etc/network/interfaces` in a text editor:

```
sudo nano /etc/network/interfaces
```

Then append the define appropriate stanzas for your wireless interface, along with the SSID and PSK. For example:

<pre>
# WiFi
auto wlan0
iface wlan0 inet dhcp
wpa-ssid NNNN
wpa-psk NNNN
</pre>

The `auto` stanza will bring your interface up at system startup.

* **wpa-ssid** - your wifi name
* **wpa-psk** - your wifi password

**4.** We can now bring our interface up and down with the usual `ifup` and `ifdown` commands:

```
sudo ifup wlan0
```

This will start `wpa_supplicant` as a background process.

If you added `auto wlan0` as in the example above, the interface should be brought up automatically during boot up.
