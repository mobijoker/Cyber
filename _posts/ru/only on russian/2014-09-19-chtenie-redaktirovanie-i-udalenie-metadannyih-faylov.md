---
id: 472
lang: ru
ref: chtenie-redaktirovanie-i-udalenie-metadannyih-faylov
title: Чтение, редактирование и удаление метаданных файлов
date: 2014-09-19T14:23:24+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=472
permalink: /ru/linux/chtenie-redaktirovanie-i-udalenie-metadannyih-faylov.html
categories:
  - Debian/Ubuntu
  - Linux
  - Mac OS
  - Raspberry Pi
tags:
  - anonymity
  - exif
  - meta
  - meta-data
  - metadata
  - метаданные

---

![thumb](/images/attachment-icon-150x150.png)
Многие форматы файлов могут содержать метаданные. Существуют разные типы метаданных. Большинство цифровых фото/видеокамер и мобильных телефонов добавляют EXIF метаданные в фотографии и видеофайлы. Метаданные могут содержать информацию об устройстве, его настройки, местоположение (координаты GPS) и многое другое.


Перед публикацией в сеть каких-либо файлов необходимо, при возможности, удалить из них все метаданные, таким образом позаботившись о приватности. Для этого можно воспользоваться консольной программой <a href="http://owl.phy.queensu.ca/~phil/exiftool/" target="_blank">ExifTool</a> от Phil Harvey.


### Метаданные поддерживаемые ExifTool

Ниже список типов файлов и метаданных поддерживаемых ExifTool (`r` = чтение, `w` = запись, `c` = создание).

Поддерживаемые типы файлов :

<pre>
         File Types :
         ------------+-------------+-------------+-------------+-----------
         3FR   r     | DVB   r     | M4A/V r     | PBM   r/w   | RWL   r/w
         3G2   r     | DYLIB r     | MEF   r/w   | PDF   r/w   | RWZ   r
         3GP   r     | EIP   r     | MIE   r/w/c | PEF   r/w   | RM    r
         ACR   r     | EPS   r/w   | MIFF  r     | PFA   r     | SO    r
         AFM   r     | ERF   r/w   | MKA   r     | PFB   r     | SR2   r/w
         AI    r/w   | EXE   r     | MKS   r     | PFM   r     | SRF   r
         AIFF  r     | EXIF  r/w/c | MKV   r     | PGF   r     | SRW   r/w
         APE   r     | F4A/V r     | MNG   r/w   | PGM   r/w   | SVG   r
         ARW   r/w   | FLA   r     | MOS   r/w   | PICT  r     | SWF   r
         ASF   r     | FLAC  r     | MOV   r     | PMP   r     | THM   r/w
         AVI   r     | FLV   r     | MP3   r     | PNG   r/w   | TIFF  r/w
         BMP   r     | FPX   r     | MP4   r     | PPM   r/w   | TTC   r
         BTF   r     | GIF   r/w   | MPC   r     | PPT   r     | TTF   r
         COS   r     | GZ    r     | MPG   r     | PPTX  r     | VRD   r/w/c
         CR2   r/w   | HDP   r/w   | MPO   r/w   | PS    r/w   | VSD   r
         CRW   r/w   | HTML  r     | MQV   r     | PSB   r/w   | WAV   r
         CS1   r/w   | ICC   r/w/c | MRW   r/w   | PSD   r/w   | WDP   r/w
         DCM   r     | IIQ   r/w   | MXF   r     | PSP   r     | WEBP  r
         DCP   r/w   | IND   r/w   | NEF   r/w   | QTIF  r     | WEBM  r
         DCR   r     | ITC   r     | NRW   r/w   | RA    r     | WMA   r
         DFONT r     | JNG   r/w   | NUMBERS r   | RAF   r/w   | WMV   r
         DIVX  r     | JP2   r/w   | ODP   r     | RAM   r     | X3F   r/w
         DJVU  r     | JPEG  r/w   | ODS   r     | RAR   r     | XCF   r
         DLL   r     | K25   r     | ODT   r     | RAW   r/w   | XLS   r
         DNG   r/w   | KDC   r     | OGG   r     | RIFF  r     | XLSX  r
         DOC   r     | KEY   r     | ORF   r/w   | RSRC  r     | XMP   r/w/c
         DOCX  r     | LNK   r     | OTF   r     | RTF   r     | ZIP   r
         DV    r     | M2TS  r     | PAGES r     | RW2   r/w   |
</pre>

Поддерживаемые стандарты и типы метаданных :

<pre>
         Meta Information :
         ----------------------+----------------------+---------------------
         EXIF           r/w/c  |  CIFF           r/w  |  Ricoh RMETA    r
         GPS            r/w/c  |  AFCP           r/w  |  Picture Info   r
         IPTC           r/w/c  |  Kodak Meta     r/w  |  Adobe APP14    r
         XMP            r/w/c  |  FotoStation    r/w  |  MPF            r
         MakerNotes     r/w/c  |  PhotoMechanic  r/w  |  Stim           r
         Photoshop IRB  r/w/c  |  JPEG 2000      r    |  APE            r
         ICC Profile    r/w/c  |  DICOM          r    |  Vorbis         r
         MIE            r/w/c  |  Flash          r    |  SPIFF          r
         JFIF           r/w/c  |  FlashPix       r    |  DjVu           r
         Ducky APP12    r/w/c  |  QuickTime      r    |  M2TS           r
         PDF            r/w/c  |  Matroska       r    |  PE/COFF        r
         PNG            r/w/c  |  GeoTIFF        r    |  AVCHD          r
         Canon VRD      r/w/c  |  PrintIM        r    |  ZIP            r
         Nikon Capture  r/w/c  |  ID3            r    |  (and more)
</pre>


### Устанока ExifTool

Для «ExifTool» требуется «Perl» версии 5.004 или новее. Никакие другие библиотеки не требуются.

Для установки «ExifTool» на «Debian», «Ubuntu» или «Linux Mint»:

```
sudo apt-get install libimage-exiftool-perl
```

Для установки «ExifTool» на «Fedora»:

```
sudo yum install perl-Image-ExifTool
```

Для установки «ExifTool» на «CentOS» или «RHEL», сначала нужно подключить репозиторий «EPEL», а затем:

```
sudo yum install perl-Image-ExifTool
```

Для установки «ExifTool» на Mac OS нужно скачать установщик с оф-сайта: [http://owl.phy.queensu.ca/~phil/exiftool/](http://owl.phy.queensu.ca/~phil/exiftool/)

Ещё «ExifTool» можно установить как модуль «Perl».


### Чтение метаданных файла

Прочитать все метаданные файла:

```
exiftool input.jpg
```

Прочитать информацию о GPS координатах фотографии :

```
exiftool -gpslatitude -gpslongitude input.jpg
```

Пример вывода:

<pre>
GPS Latitude : 54 deg 9' 42.68" N
GPS Longitude : 5 deg 58' 35.93" W
</pre>

Для отображения информации о GPS координатах содержащихся в фотографии в форматированном виде:

```
exiftool -filename -gpslatitude -gpslongitude -T input.jpg
```

Пример вывода:

<pre>
input.jpg 54 deg 9' 42.68" N 5 deg 58' 35.93" W
</pre>


### Изменение метаданных файла

При внесении изменений в файлы ExifTool автоматически сохраняет копии оригинальных файлов, добавляя к их именам префикс `_original`. Для того, чтобы бэкапы не создавались нужно добавлять параметр `-overwrite_original` к командам. Для удаления созданного бэкапа нужно добавлять параметр `-delete_original[!]`, а для восстановления из бэкапа `-restore_original`. Ещё может понадобится параметр `-progress` для отображения прогресса и `-r` для рекурсивной обработки.

Изменить теги "Title" и "Author":

```
exiftool -Title="This is the title" -Author="Arthur Gareginyan" input.pdf
```

Изменить тэги нескольких файлов:

```
exiftool -copyright="2014 Arthur Gareginyan" a.jpg b.jpg c.jpg
```

Изменить тег "artist" для всех файлов в директории назначения:

```
exiftool -artist="Arthur Gareginyan" ./folder
```


### Удаление метаданных файла

Удалить все метаданные из файла:

```
exiftool -all= input.jpg
```

Удалить метаданные из всех файлов с расширением `.jpg` в текущей директории:

```
exiftool -all= *.jpg
```

Удалить метаданные из всех файлов в текущей директории:

```
exiftool -all= *
```

Если нужно удалить метаданные рекурсивно из всех файлов в директории `/home/user/photo/`, не создавая бэкапы и с показам прогресса:

```
exiftool -overwrite_original -progress -r -all=  /home/user/photo/*
```

**Примечание:**
Существует множество типов метаданных и ExifTool удаляет только те метаданные с которыми умеет работать!
