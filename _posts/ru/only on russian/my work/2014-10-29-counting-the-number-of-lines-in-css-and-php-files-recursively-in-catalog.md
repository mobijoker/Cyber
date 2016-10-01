---
lang: ru
ref: counting-the-number-of-lines-in-css-and-php-files-recursively-in-catalog
title: Counting the number of lines in CSS and PHP files, recursively in catalog
date: 2014-10-29T14:19:54+00:00
author: Arthur Gareginyan
layout: post
permalink: /ru/linux/counting-the-number-of-lines-in-css-and-php-files-recursively-in-catalog.html
categories:
  - Debian/Ubuntu
  - Linux
  - Mac OS
  - Raspberry Pi
  - Мои программы
tags:
  - counting
  - lines
  - linux
  - mac
  - mac os
  - number

---

![thumb](/images/thumbnail/bash.png)
Временами бывает нужно посчитать количество строк кода в написанном проекте. Для этого Я написал сценарий на "BASH" который считает количество строк во всех файлах с "PHP" и "CSS" расширением найденных в указанном каталоге и его подкаталогах (рекурсивно).

<br><br>

Код написан под поиск "PHP" и "CSS" файлов но может быть легко переделан под другие типы файлов.


### Code

**Name:** num_lines.sh

**Description:** Counting the number of lines in CSS and PHP files, recursively in catalog.

**Language:** BASH

```bash
#!/bin/bash
#=============================================================#
# Name:         Counting the number of lines                  #
# Description:  Counting the number of lines in CSS and PHP   #
#               files, recursively in catalog.                #
# Version:      1.1                                           #
# Data:         7.2.2014-28.10.2014                           #
# Author:       Arthur (Berserkr) Gareginyan                  #
# Author URI:   http://mycyberuniverse.com/author.html        #
# Email:        arthurgareginyan@gmail.com                    #
# License:      GNU General Public License, version 3 (GPLv3) #
# License URI:  http://www.gnu.org/licenses/gpl-3.0.html      #
#=============================================================#
 
#                   USAGE:
#       ~/num_lines.sh /example_directory


################### SETUP VARIABLES #######################
place="$1"


################## DECLARE FUNCTIONS ######################

# Поиск файлов PHP и вывод списка
function listPHPFiles() {
	list_php=`find ./ -name "*php"`
	for php_file in $list_php
	do
	        echo $php_file
	done
}

# Поиск файлов CSS и вывод списка
function listCSSFiles() {
	list_css=`find ./ -name "*css"`
	for css_file in $list_css
	do
	        echo $css_file
	done
}

# Подсчёт PHP файлов
function countingPHPFiles() {
	count=$(find ./ -name "*php" | wc -l | sed 's/^ *//')
	PHPFiles=$count
}

# Подсчёт CSS файлов
function countingCSSFiles() {
	count=$(find ./ -name "*css" | wc -l | sed 's/^ *//')
	CSSFiles=$count
}

# Сложение всех строк
function additionFiles() {
	numFiles=$[$PHPFiles+$CSSFiles]
}

# Подсчёт строк в PHP файлах
function countingPHPLines() {
	for php_file in $list_php
	do
	        cmd_php=`awk 'END { print NR }' $php_file`
	        num_php=$[$num_php+$cmd_php]
	done
}

# Подсчёт строк в CSS файлах
function countingCSSLines() {
	for css_file in $list_css
	do
	        cmd_css=`awk 'END { print NR }' $css_file`
	        num_css=$[$num_css+$cmd_css]
	done
}

# Сложение всех строк
function additionLines() {
	numLines=$[$num_php+$num_css]
}

######################## GO ###############################
# Переход в рабочюю директорию
pushd $place >/dev/null 2>&1

echo -e "\nLIST OF All FOUNDED FILES:"
listPHPFiles
listCSSFiles
countingPHPFiles
countingCSSFiles
additionFiles
countingPHPLines
countingCSSLines
additionLines

popd >/dev/null 2>&1

# Результат
echo -e "\nIN $PHPFiles PHP FILES: $num_php lines"
echo -e "IN $CSSFiles CSS FILES: $num_css lines"
echo -e "\nIN ALL $numFiles FILES: $numLines lines"

exit 0
```


### Usage

Run the num_lines.sh with path to needed directory: 

```sh
~/num_lines.sh /example_directory
```


### Output

<pre>
LIST OF All FOUNDED FILES:
.//index.php
.//page.php
.//style.css

IN 2 PHP FILES: 230 lines
IN 1 CSS FILES: 292 lines

IN ALL 3 FILES: 522 lines
</pre>

<br/>
{% assign url = "https://github.com/ArthurGareginyan/counting-number-of-lines" %}{% include button-github.html %}