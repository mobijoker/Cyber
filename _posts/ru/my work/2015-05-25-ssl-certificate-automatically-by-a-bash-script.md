---
lang: ru
ref: ssl-certificate-automatically-by-a-bash-script
title: 'SSL сертификат автоматически при помощи BASH сценария'
date: 2015-05-25T23:06:27+00:00
author: Arthur Gareginyan
layout: post
permalink: /ru/linux/ssl-certificate-automatically-by-a-bash-script.html
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
Для быстрого и лёгкого создания самоподписанных SSL сертификатов для вэб-серверов Apache и Nginx Я написал не большой сценарий на «BASH».


SSL сертификаты необходимы для обеспечения безопасной передачи информации в сети.  В криптографии и компьютерной безопастности под самоподписанным SSL сертификатом понимают сертификат открытого ключа, изданный и подписанный тем же лицом, которое он идентифицирует. То есть, если вы сами, для своего домена или IP-адреса, создали SSL сертификат то он будет называться самоподписанным. Самоподписанные SSL сертификаты лучше всего подходят для внутреннего пользования (интранет).

* **Название:** SSL Certificate Creater (ssl_crt_creater.sh)
* **Описание:** Create a self-signed SSL Certificates for Apache and Nginx web-servers.
* **Язык:** BASH

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


### Использование

Перед запуском сценария необходимо установить права на исполнение:

```sh
chmod +x ssl_crt_creater.sh
```

Запуск сценария:

```sh
./ssl_crt_creater.sh
```

После создания SSL сертификата, следует самостоятельно привязать его к серверу.

Скриншот меню сценария:
<img class="aligncenter" src="/images/ssl-certificate-automatically-by-a-bash-script/ssl_crt_creater.png" alt="SSL Certificate Creater" />


### Описание

Для выполнения сценария требуется наличие пакетов `dialog` и `openssl`. Пакет `dialog` используется для визуализации меню, а при помощи пакета `openssl` создаётся сертификат. Если они не установлены то сценарий предложит их установить самостоятельно. 

В сценарии, для создания сертификата и ключа, используется такая команда для NginX:

<pre>
openssl req -new -x509 -days 365 -nodes -out /etc/nginx/ssl/$__servername.crt -keyout /etc/nginx/ssl/$__servername.key
</pre>

и такая для Apache:

<pre>
openssl req -new -x509 -days 365 -nodes -out /etc/apache2/ssl/$__servername.crt -keyout /etc/apache2/ssl/$__servername.key
</pre>

Описание аргументов:
`req` - Запрос на создание нового сертификата.
`-new` - Создание запроса на сертификат (Certificate Signing Request – далее CSR).
`-x509` - Вместо создания CSR (см. опцию -new) создать самоподписанный сертификат.
`-days 365` - Срок действия сертификата 365 дней (1 год).
`-nodes` - Не шифровать закрытый ключ.
`-out` - Место сохранения сертификата.
`-keyout` - Место сохранения закрытого ключа.

После выполнения сценария будет автоматически создан новый сертификат и закрытый RSA ключ длиной 2048 бит. Они будут помещены в рабочую директорию (Apache - `/etc/apache2/ssl/`, NginX - `/etc/nginx/ssl/`) и на них будут установлены права `600` для безопасности.

Теперь закрытый ключ и самоподписанный сертификат находятся сдесь:

<pre>
/etc/apache2/ssl/*.crt и /etc/apache2/ssl/*.key
</pre>

или здесь:

<pre>
/etc/nginx/ssl/*.crt и /etc/nginx/ssl/*.key
</pre>

<br/>
{% assign url = "https://github.com/ArthurGareginyan/SSL-Certificate-Creater" %}{% include button-github.html %}
