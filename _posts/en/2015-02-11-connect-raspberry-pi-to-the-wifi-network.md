---
id: 534
lang: en
ref: connect-raspberry-pi-to-the-wifi-network
title: Connect Raspberry Pi to the WiFi network
date: 2015-02-11T05:43:42+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=534
permalink: /linux/connect-raspberry-pi-to-the-wifi-network.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - connect
  - debian.ubuntu
  - raspberry
  - raspberrypi
  - raspbian
  - wifi
  - wifi dongle

---

![thumb](/images/WiFi1-300x300.png)
By default the Raspberry Pi uses DHCP to configure its network interfaces, including, on the model B, the built-in ethernet port. In this post I'll cover how you can set up your Raspberry Pi to automatically connect to your wireless network and obtain a static IP or configure WPA2 using wpa_supplicant. All you need is a WiFi dongle.


### SETUP THE WIFI INTERFACE

I have a new "ASUS USB-N10" 802.11b/g/n USB WiFi dongle with the chip “Realtek 8192cu” (used in many adapters). This dongle needs the firmware-realtek package which is preinstalled in the newer Rasbian releases. So just need to plug it into the USB port and it will work.

Note that a WiFi dongle will probably need more power than the Raspberry Pi USB port can provide, especially if there is a large distance from the WiFi dongle to the WiFi Access Point, or it is transferring large amounts of data. Therefore, you may need to plug the WiFi dongle into a powered USB hub. But "ASUS USB-N10" is working fine.

First we'll make sure the dongle is recognized:

```
lsusb
```

<pre>
Bus 001 Device 002: ID 0424:9512 Standard Microsystems Corp.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 003: ID 0424:ec00 Standard Microsystems Corp.
Bus 001 Device 004: ID 0b05:17ba ASUSTek Computer, Inc.
</pre>

As you can see, my ASUS dongle is on the last line.

Now run lsmod to see avaliable kernel modules, hopefully we'll see something that matches our chip:

```
lsmod
```

<pre>
Module Size Used by
snd_bcm2835 21342 0
snd_pcm 93100 1 snd_bcm2835
snd_seq 61097 0
snd_seq_device 7209 1 snd_seq
snd_timer 23007 2 snd_pcm,snd_seq
snd 67211 5 snd_bcm2835,snd_timer,snd_pcm,snd_seq,snd_seq_device
8192cu 569585 0
uio_pdrv_genirq 3666 0
uio 9897 1 uio_pdrv_genirq
</pre>

The interesting module is third last (8192cu).

Now do a WiFi scan to see working it or no:

```
iwlist wlan0 scan
```

**Note:** Your Wi-Fi dongle may have a name `wlan1` instead of `wlan0`.


### SETUP THE WIFI NETWORK

First need is add a network configuration to the file `/etc/wpa_supplicant/wpa_supplicant.conf`.

Open up the `/etc/wpa_supplicant/wpa_supplicant.conf` file:

```
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

Edit it so that, it will look like this:

<pre>
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
     ssid="Your SSID Here"
     psk="Enter Passkey Here"
     proto=RSN
     key_mgmt=WPA-PSK
     pairwise=CCMP TKIP
     group=CCMP TKIP
}
</pre>

or, if you use more then one network configuration, it will look like this:

<pre>
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
     ssid="Your SSID Here"
     psk="Enter Passkey Here"
     proto=RSN
     key_mgmt=WPA-PSK
     pairwise=CCMP TKIP
     group=CCMP TKIP
     id_str="home"
     priority=1
}

network={
     ssid="Your SSID Here"
     psk="Enter Passkey Here"
     proto=RSN
     key_mgmt=WPA-PSK
     pairwise=CCMP TKIP
     group=CCMP TKIP
     id_str="work"
     priority=2
}
</pre>

* **said** - name of SSID
* **psk** - passkey
* **proto** - could be either RSN (WPA2) or WPA (WPA1).
* **key_mgmt** - could be either WPA-PSK (most probably) or WPA-EAP (enterprise networks)
* **pairwise** - could be either CCMP (WPA2) or TKIP (WPA1)
* **group** - could be either CCMP (WPA2) or TKIP (WPA1)
* **id_str** - name of configuration
* **priority** - priority of network

After you have modified the `wpa_supplicant.conf` file, you will need to change the `wlan0` section of the `/etc/network/interfaces` file.

Open up the `/etc/network/interfaces` file:

```
sudo nano /etc/network/interfaces
```

Edit the `wlan0` section so that, for a static IP, it will look like this:

<pre>
### WiFi
#allow-hotplug wlan0
iface wlan0 inet manual
     wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf
iface default inet static
     address 192.168.1.2
      netmask 255.255.255.0
      network 192.168.1.0
      gateway 192.168.1.1
</pre>

And for DHCP, it will look like this:

<pre>
### WiFi
#allow-hotplug wlan0
iface wlan0 inet manual
     wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf
iface default inet dhcp
</pre>

or if you use more then one network configuration:

<pre>
### WiFi
#allow-hotplug wlan0
iface wlan0 inet manual
     wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf
iface default inet dhcp
iface home inet dhcp
iface work inet dhcp
</pre>

After that, you will need to bring down the `wlan0` interface and then back it up:

```
sudo ifdown wlan0
sudo ifup wlan0
```

Now you can check the wireless connection using the `iwconfig` command:

```
iwconfig
```

<pre>
wlan0 IEEE 802.11bgn ESSID:"Your SSID Here" Nickname:"&lt;WIFI@REALTEK&gt;"
Mode:Managed Frequency:2.412 GHz Access Point: NN:NN:NN:NN:NN:NN
Bit Rate:150 Mb/s Sensitivity:0/0
Retry:off RTS thr:off Fragment thr:off
Power Management:off
Link Quality=98/100 Signal level=60/100 Noise level=0/100
Rx invalid nwid:0 Rx invalid crypt:0 Rx invalid frag:0
Tx excessive retries:0 Invalid misc:0 Missed beacon:0

lo no wireless extensions.

eth0 no wireless extensions.
</pre>


### WHAT WE GET

**1.** During bootup, `wpa_supplicant` searches through each network we have listed with a specific priority in the file `wpa_supplicant.conf`, then chooses the first active network it finds.

**2.** If there is no WiFi dongle connected, it uses the wired connection `eth0`.

**3.** We can now connect to my router that have a hidden SSID (SSID not broadcasted), which was not possible with just the `/etc/network` file by itself without using `wpa_supplicant.conf`. I disable broadcasts for security reasons.

**4.** The `wpa_supplicant` file does not think that the character `\` is an escape character in the password field, unlike the `/etc/network` file by itself without using `wpa_supplicant.conf`, which required that it be escaped with another escape character `\\`.
