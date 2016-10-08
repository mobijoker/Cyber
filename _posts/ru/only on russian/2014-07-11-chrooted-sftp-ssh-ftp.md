---
lang: ru
ref: chrooted-sftp-ssh-ftp
title: Chrooted SFTP (SSH FTP)
date: 2014-07-11
author: Arthur Gareginyan
translator: Arthur Gareginyan
layout: post
permalink: /ru/linux/chrooted-sftp-ssh-ftp.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - chroot
  - FTP
  - OpenSSH
  - SFTP
  - sshd

---

![thumb]()
Сервер `sshd` (OpenSSH) позволяет осуществлять доступ по протоколу SFTP. «OpenSSH» по умолчанию даёт пользователю доступ ко всей файловой системе, тоесть к корню. Но можно chroot-нуть пользователя в его домашнюю директорию. Тоесть юзер будет заперт в своей домашней директории.
 

Начиная с версии 4.8, «OpenSSH» поддерживает `chroot` (http://openssh.org/txt/release-4.8) и теперь не нужны патчи.


### Подготовка

Право входа в систему по протоколу SFTP будут иметь юзеры имеющие системные учётные записи. В примере Я буду использовать имя юзера `Arthur` с домашней директорией в `/home/Arthur`. Юзер `Arthur` входит в группу `users`.

Если необходимый юзер ещё не существует, то создадим:

```sh
adduser Arthur
```

Создадим группу:

```sh
groupadd users
```

Добавим юзера `Arthur` в группу `users`:

```sh
useradd -G users Arthur
```


### Установка OpenSSH

Если OpenSSH ещё не установлен:

```sh
apt-get install ssh openssh-server
```


### Включение chrooted SFTP

Для включения SFTP откроем файл настройки OpenSSH сервера:

```sh
nano /etc/ssh/sshd_config
```

и убедимся в том, что имеется одна из этих строк:

```
Subsystem sftp /usr/lib/openssh/sftp-server
```

или:

```
Subsystem sftp internal-sftp
```

Затем добавим следующий блок в конец файла (для каждого юзера которого хотим chroot-ить необходим отдельный блок):

<pre>
Match User Arthur
    ChrootDirectory /home
    AllowTCPForwarding no
    X11Forwarding no
    ForceCommand /usr/lib/openssh/sftp-server
</pre>

**Примечание:**
`ChrootDirectory` - владельцем этого каталога должен быть `root` и у других юзеров не должно быть прав на запись. Поэтому `ChrootDirectory` делается на каталог выше, где у юзеров нет прав на запись, а уже внутри каталога `/home/Arthur` у него есть права на запись.

Если юзеров много, тогда можно chroot-нуть группу в которую входят все юзеры:

<pre>
Match Group users
    ChrootDirectory /home
    AllowTCPForwarding no
    X11Forwarding no
    ForceCommand /usr/lib/openssh/sftp-server
</pre>

**Примечание:**
`Match` - поддерживает «User», «Group», «Host» и «Address» - для гибкой и групповой настройки.

Тоесть все входящие в группу `users` будут chroot-ится в директорию `/home`.

Перезапустим OpenSSH:

```sh
sudo /etc/init.d/ssh restart
```

или так:

```sh
sudo service ssh restart
```

Если мы chroot-им разных юзеров в одну директорию но не хотим, чтобы они гуляли по домашним директориям других юзеров, тогда нужно изменить права на каждую домашнюю директорию:

```sh
chmod 700 /home/Arthur
```

Теперь можно подключится к нашему хосту по протоколу SFTP.
