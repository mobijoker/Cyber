---
lang: ru
ref: how-to-fix-setting-locale-failed
title: 'Как исправить: "Setting locale failed."'
date: 2015-10-05
author: Arthur Gareginyan
translator: Arthur Gareginyan
layout: post
permalink: /ru/error/how-to-fix-setting-locale-failed.html
categories:
  - Error
tags:
  - en_US
  - en_US.UTF-8
  - error
  - issue
  - locale
  - locale-gen
  - ru_RU
  - ru_RU.UTF-8

---

![thumb](/images/thumbnail/error.png)
В различных ситуациях (например, во время установки приложений Perl или при использовании `apt-get install`) я получаю следующее предупреждающее сообщение:

<pre>
perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
	LANGUAGE = (unset),
	LC_ALL = (unset),
	LC_CTYPE = "UTF-8",
	LANG = "ru_RU.UTF-8"
    are supported and installed on your system.
perl: warning: Falling back to the standard locale ("C").
locale: Cannot set LC_CTYPE to default locale: No such file or directory
locale: Cannot set LC_ALL to default locale: No such file or directory
</pre>


Это предупреждение означает, что вы не настроили правильно локали (языковые стандарты) в вашей системе. Для устранения этой проблемы необходимо выполнить следующие действия.


### Проверка локалей

Проверьте, какие языки в настоящее время созданы используя `locale -a`:

```sh
locale -a
```

<pre>
locale: Cannot set LC_CTYPE to default locale: No such file or directory
locale: Cannot set LC_ALL to default locale: No such file or directory
C
C.UTF-8
POSIX
ru_RU.utf8
</pre>

И/или используя `locale`:

```sh
locale
```

<pre>
LANG=ru_RU.UTF-8
LANGUAGE=
LC_CTYPE="ru_RU.UTF-8"
LC_NUMERIC="ru_RU.UTF-8"
LC_TIME="ru_RU.UTF-8"
LC_COLLATE="ru_RU.UTF-8"
LC_MONETARY="ru_RU.UTF-8"
LC_MESSAGES="ru_RU.UTF-8"
LC_PAPER="ru_RU.UTF-8"
LC_NAME="ru_RU.UTF-8"
LC_ADDRESS="ru_RU.UTF-8"
LC_TELEPHONE="ru_RU.UTF-8"
LC_MEASUREMENT="ru_RU.UTF-8"
LC_IDENTIFICATION="ru_RU.UTF-8"
LC_ALL=
</pre>

Программы, которые поддерживают технологию локализации используют переменные среды для определения конвенции для применения форматирования даты и времени, отображения символов, местной валюты и кодировки страницы.

Следующие переменные среды влияют на поведение системы связанное с локалью:

* LANG - Определяет язык по умолчанию в отсутствие других языков связанных с переменными среды.
* LANGUAGE - 
* LC_ADDRESS - Конвенция используется для форматирования уличных или почтовых адресов.
* LC_ALL - Высокий приоритет переопределения для конкретных языковых стандартов поведения (переопределяет все другие переменные).
* LC_COLLATE - Порядок сортировки.
* LC_CTYPE - Классификация символов и преобразование регистра.
* LC_MONETARY - Денежное форматирование.
* LC_MEASUREMENT - Стандартные системы измерения, используемые в регионе.
* LC_MESSAGES - Формат интерактивных слов и ответов.
* LC_NUMERIC - Числовое форматирование.
* LC_PAPER - Стандартный размер страницы для региона.
* LC_RESPONSE - Определяет ответы (такие какs Да и Нет) на местном языке.
* LC_TELEPHONE - Конвенция используется для представления телефонных номеров.
* LC_TIME - Форматы даты и времени.


### Настройка локалей

Чтобы увидеть, какие языки поддерживаются используйте:

```sh
less /usr/share/i18n/SUPPORTED
```

Вы увидите длинный список названий локалей пригодные для использования в переменных среды. В этом списке найдите нужный вам язык, например «en»:

<pre>
en_US
en_US.UTF-8
</pre>

Теперь вам нужно сгенерировать эти локали. Вы можете сделать это с помощью `locale-gem`:

```sh
sudo locale-gen en_US.UTF-8
```

<pre>
Generating locales (this might take a while)...
  en_US.UTF-8... done
Generation complete.
</pre>

В качестве альтернативы файл локали может быть создан вручную с `localedef`:

```sh
sudo localedef -i en_US -f UTF-8 en_US.UTF-8
```

Это должно создать локали и затем пере-настроить их.

Выполните команду `locale -a` для проверки списка доступных локалей (обратите внимание на изменение синтаксиса):

```sh
locale -a
```

<pre>
C
C.UTF-8
en_US.utf8
POSIX
ru_RU.utf8
</pre>

Проверьте новые локали:

```sh
locale
```

<pre>
LANG=en_US.UTF-8
LANGUAGE=en_US.UTF-8
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=en_US.UTF-8
</pre>

Для использования новых параметров с вашими программами, необходимо пере-логинится (выйти и войти обратно) или перезагрузить систему.
