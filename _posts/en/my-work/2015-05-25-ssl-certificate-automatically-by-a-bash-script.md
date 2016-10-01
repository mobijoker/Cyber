---
lang: en
ref: ssl-certificate-automatically-by-a-bash-script
title: SSL Certificate automatically by a BASH script
date: 2015-05-25T23:06:27+00:00
author: Arthur Gareginyan
layout: post
permalink: /linux/ssl-certificate-automatically-by-a-bash-script.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
  - Мои программы
  - my-work
tags:
  - apache
  - certificate
  - crt
  - nginx
  - self-signed
  - ssl
  - самоподписанный
  - сертификат

---

![thumb](/images/thumbnail/bash.png)
To quickly and easily create a self-signed SSL certificate for Web servers Apache and Nginx I wrote a little script in "BASH".

<br><br>

SSL certificates are required to ensure the secure transfer of information in the network. In cryptography and computer security, a self-signed certificate is an identity certificate that is signed by the same entity whose identity it certifies. That is, if you yourself, for your domain or IP address, created the SSL certificate it will be self-signed. Self-signed SSL certificates are ideal for internal use (intranet).

* **Name:** SSL Certificate Creater (`ssl_crt_creater.sh`)
* **Description:** Create a self-signed SSL Certificates for Apache and Nginx web-servers.
* **Language:** BASH

```bash
#!/bin/bash
#=============================================================#
# Name:         SSL Certificate Creater                       #
# Description:  Create a self-signed SSL Certificates         #
#               for Apache and Nginx web-servers.             #
# Version:      1.1                                           #
# Data:         30.10.2014                                    #
# Author:       Arthur (Berserkr) Gareginyan                  #
# Author URI:   http://mycyberuniverse.com/author.html        #
# Email:        arthurgareginyan@gmail.com                    #
# License:      GNU General Public License, version 3 (GPLv3) #
# License URI:  http://www.gnu.org/licenses/gpl-3.0.html      #
#=============================================================#

#                   USAGE:
#      chmod +x ./ssl_crt_creater.sh
#      sudo ./ssl_crt_creater.sh


################## DECLARE FUNCTIONS ######################

checkRoot() {
   if [ $(id -u) -ne 0 ]; then
     printf "Script must be run as root. Try 'sudo ./ssl_certificate_creater.sh'\n"
     exit 1
   fi
}

checkNeededPackages() {
   lst="dialog openssl"
   for items in $lst
   do
     type -P $items &>/dev/null || {
       echo -en "\n Package \"$items\" is not installed!"
       echo -en "\n Install now? [yes]/[no]: "
       read ops
       case $ops in
           YES|yes|Y|y) sudo apt-get install $items ;;
           	     *)  echo -e "\n Exiting..."
               		 exit 1 ;;
       esac
     }
   done
}

setServerName() {
    cmd=(dialog --backtitle "mycyberuniverse.com - Create SSL Certificate for NGinX/Apache" \
		--inputbox "\n Please enter the URL of your website." 22 76 $__servername)
    choices=$("${cmd[@]}" 2>&1 >/dev/tty)
    if [ "$choices" != "" ]; then
        __servername=$choices
    else
        break
    fi
}

checkServerName() {
   if [ "$__servername" = "" ]; then
         setServerName
   fi
}

installCertificateNginx() {
  dialog --backtitle "mycyberuniverse.com - Create SSL Certificate for NGinX/Apache" \
         --title "Create SSL Certificate for NGinX" \
	 --msgbox "\n We are now going to create a self-signed certificate. While you could simply press ENTER when you are asked for country name etc. or enter whatever you want, it might be beneficial to have the web servers host name in the common name field of the certificate." 20 60
  mkdir -p /etc/nginx/ssl
  openssl req -new -x509 -days 365 -nodes -out /etc/nginx/ssl/$__servername.crt -keyout /etc/nginx/ssl/$__servername.key
  chmod 600 /etc/nginx/ssl/$__servername.key
  dialog --backtitle "mycyberuniverse.com - Create SSL Certificate for NGinX/Apache" \
         --title "Create SSL Certificate for NGinX" \
         --msgbox "\n Done! Your certificates are available at /etc/nginx/ssl/$__servername.crt & /etc/nginx/ssl/$__servername.key" 20 60
}

installCertificateApache() {
  dialog --backtitle "mycyberuniverse.com - Create SSL Certificate for NGinX/Apache" \
         --title "Create SSL Certificate for Apache" \
	 --msgbox "\n We are now going to create a self-signed certificate. While you could simply press ENTER when you are asked for country name etc. or enter whatever you want, it might be beneficial to have the web servers host name in the common name field of the certificate." 20 60
  clear
  mkdir -p /etc/apache2/ssl
  openssl req -new -x509 -days 365 -nodes -out /etc/apache2/ssl/$__servername.crt -keyout /etc/apache2/ssl/$__servername.key
  chmod 600 /etc/apache2/ssl/$__servername.key
  dialog --backtitle "mycyberuniverse.com - Create SSL Certificate for NGinX/Apache" \
         --title "Create SSL Certificate for Apache" \
         --msgbox "\n Done! Your certificates are available at /etc/apache2/ssl/$__servername.crt & /etc/apache2/ssl/$__servername.key" 20 60
}


######################## GO ###############################

checkRoot
checkNeededPackages

while true; do
    cmd=(dialog --backtitle "mycyberuniverse.com - Create SSL Certificate for NGinX/Apache" \
                --title "Create SSL Certificate for NGinX/Apache" \
                --menu "You MUST set the server URL (e.g., myaddress.dyndns.org) before starting create certificate. Choose task:" 20 60 15)
    options=(1 "Set server URL ($__servername)"
             2 "Generate new SSL certificate for NGiNX"
             3 "Generate new SSL certificate for Apache"
             4 "Exit")
    choice=$("${cmd[@]}" "${options[@]}" 2>&1 >/dev/tty)
    if [ "$choice" != "" ]; then
        case $choice in
            1) setServerName ;;
            2) checkServerName
               installCertificateNginx ;;
            3) checkServerName
               installCertificateApache ;;
            4) clear
               exit 0 ;;
        esac
    else
        break
    fi
done
clear

exit 0
```


### Use

Before you run the script, you must set the performance rights:

```sh
chmod +x ssl_crt_creater.sh
```

Run the script:

```sh
./ssl_crt_creater.sh
```

After you create the SSL certificate then you should bind it to the server.

A screenshot of the menu of script:
<img class="aligncenter" src="/images/ssl-certificate-automatically-by-a-bash-script/ssl_crt_creater.png" alt="SSL Certificate Creater" />


### Description

To run the script required packages `dialog` and `openssl`. Package `dialog` is used to render the menu and package `openssl` is used to create certificate. If they are not installed then the script will prompt you to install them. 

In the script, to create the certificate and key is used, this command for NginX:

<pre>
openssl req -new -x509 -days 365 -nodes -out /etc/nginx/ssl/$__servername.crt -keyout /etc/nginx/ssl/$__servername.key
</pre>

and this for Apache:

<pre>
openssl req -new -x509 -days 365 -nodes -out /etc/apache2/ssl/$__servername.crt -keyout /etc/apache2/ssl/$__servername.key
</pre>

Description of the arguments:
`req` - Request to create a new certificate.
`-new` - Creating a certificate request (Certificate Signing Request - CSR).
`-x509` - Instead of creating a CSR, create a self-signed certificate.
`-days 365` - Validity period is 365 days (1 year).
`-nodes` - Do not encrypt the private key.
`-out` - Where to store the certificate.
`-keyout` - Where to store the private key.

After running the script it will automatically create a new certificate and private RSA key length of 2048 bits. They will be placed in a working directory (Apache - `/etc/apache2/ssl/`, NginX - `/etc/nginx/ssl/`) and they will be set rights `600` for the security.

Now, your private key and certificate are available at:

<pre>
/etc/apache2/ssl/*.crt и /etc/apache2/ssl/*.key
</pre>

or at:

<pre>
/etc/nginx/ssl/*.crt и /etc/nginx/ssl/*.key
</pre>

<br/>
{% assign url = "https://github.com/ArthurGareginyan/SSL-Certificate-Creater" %}{% include button-github.html %}