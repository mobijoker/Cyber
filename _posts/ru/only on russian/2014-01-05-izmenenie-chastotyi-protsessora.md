---
id: 344
lang: ru
ref: izmenenie-chastotyi-protsessora
title: Изменение частоты процессора
date: 2014-01-05T18:10:14+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=344
permalink: /ru/linux/izmenenie-chastotyi-protsessora.html
categories:
  - Debian/Ubuntu
  - Linux

---

![thumb](/images/processor.png)
Динамическое масштабирование частоты процессора (также известное как регулирование частоты процессора) представляет собой метод в компьютерной архитектуре, где процессор работает на частоте менее максимальной в целях экономии электроэнергии (src: <a href="http://en.wikipedia.org/wiki/Dynamic_frequency_scaling">Wikipedia</a>).


---

Установите пакет <a href="http://packages.debian.org/cpufrequtils">cpufrequtils</a>:

```
apt-get install cpufrequtils
```


### Драйвер управления частотой процессора

Для корректного управления масштабированием частотой, ОС прежде всего должна знать параметры вашего процессора(ов). Для этого нужно загрузить модуль ядра, который может считывать и управлять параметрами вашего процессора(ов).

Для большинства современных ноутбуков и настольных компьютеров можно использовать драйвер `acpi-cpufreq`, но есть ещё такие варианты как `p4-clockmod`, `powernow-k6`, `powernow-k7`, `powernow-k8`, и `speedstep-centrino`.

Для загрузки драйвера вручную:


#### Intel

```
modprobe acpi-cpufreq
```

Для более старых процессоров Intel, система может выдать:
<pre>
FATAL: Error inserting acpi_cpufreq ([...]/acpi-cpufreq.ko): No such device
</pre>

В этой ситуации, замените модуль ядра `acpi_cpufreq` на `speedstep-centrino`, `p4-clockmod` или `speedstep-ich`.

**Примечание:** Учтите, что модуль `speedstep-centrino` устарел, а модуль `p4-clockmod` поддерживает только `performance` и `powersave` регуляторы.


#### AMD

```
modprobe powernow-k8
```


### Загрузка при старте системы

Для автоматической загрузки драйвера во время старта системы, добавьте соответствующий драйвер в массив `MODULES` в файле `/etc/rc.conf`. Например:

```
MODULES=( acpi-cpufreq fuse iwl3945 )
```

Как только загружен правильный драйвер `cpufreq`, вы можете посмотреть детальную информацию о вашем процессоре(ах), выполнив:

```
cpufreq-info
```

Вот пример вывода `cpufreq-info` на моём ноутбуке:

<pre>
cpufrequtils 008: cpufreq-info (C) Dominik Brodowski 2004-2009
Report errors and bugs to cpufreq @ vger.kernel.org, please.
analyzing CPU 0:
driver: acpi-cpufreq
CPUs which run at the same hardware frequency: 0
CPUs which need to have their frequency coordinated by software: 0
maximum transition latency: 10.0 us.
hardware limits: 800 MHz - 1.60 GHz
available frequency steps: 1.60 GHz, 1.33 GHz, 1.07 GHz, 800 MHz
available cpufreq governors: userspace, conservative, powersave, ondemand, performance
current policy: frequency should be within 800 MHz and 1.60 GHz.
The governor &amp;quot;ondemand&amp;quot; may decide which speed to use
within this range.
current CPU frequency is 800 MHz (asserted by call to hardware).
cpufreq stats: 1.60 GHz:0.51%, 1.33 GHz:0.09%, 1.07 GHz:0.05%, 800 MHz:99.35%  (8)
analyzing CPU 1:
driver: acpi-cpufreq
CPUs which run at the same hardware frequency: 1
CPUs which need to have their frequency coordinated by software: 1
maximum transition latency: 10.0 us.
hardware limits: 800 MHz - 1.60 GHz
available frequency steps: 1.60 GHz, 1.33 GHz, 1.07 GHz, 800 MHz
available cpufreq governors: userspace, conservative, powersave, ondemand, performance
current policy: frequency should be within 800 MHz and 1.60 GHz.
The governor &amp;quot;ondemand&amp;quot; may decide which speed to use
within this range.
current CPU frequency is 800 MHz (asserted by call to hardware).
cpufreq stats: 1.60 GHz:1.99%, 1.33 GHz:0.00%, 1.07 GHz:0.00%, 800 MHz:98.01%  (12)
</pre>

`current policy` - `ondemand`, означает то, что эта политика загружена и активна.

В большинстве случаев рекомендуется использовать именно `ondemand`.

`current CPU frequency is XXXX MHz` - если `XXXX` ниже максимальной частоты процессора то это означает, что управление частотой активно и работоспособно.

Для просмотра списка доступных регуляторов:

```
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_governors
```

Наблюдать за частотой процессора в режиме реального времени можно, выполнив команду:

```
watch grep \&amp;quot;cpu MHz\&amp;quot; /proc/cpuinfo
```


### Устранение неисправностей

* Некоторые приложения, например, `ntop`, могут некорректно работать при масштабировании частоты. В случае с `ntop` может произойти сегментация или Вы можете потерять информацию, так как регулятор `ondemand` не может достаточно быстро среагировать на повышение нагрузки на процессор и повысить частоту, а текущей частоты не хватит для обработки всех пакетов, пришедших на сетевой интерфейс.

* Некоторые модели процессоров могут не очень хорошо работать на стандартных настройках регулятора `ondemand` (например, видео воспроизводится с рывками или тормозит анимация окон). Это можно решить, не только отключив полностью масштабирование частоты. Также можно увеличить "агрессивность" переключения частоты. Просто снизьте значение переменной `up_threshold` для каждого процессора. См. изменение параметров работы регулятора `ondemand`.

* Иногда демон задает не максимальную частоту процессора, а частоту немного меньше (2.99МГц вместо 3МГц). В этой ситуации задайте значение максимальной частоты немного больше максимальной. Например, если максимальная частота процесстора 3МГц, задайте переменной `max_freq` значение 3.01МГц.

* Некоторые модели BIOS испытывают трудности с масштабированием частот, да и с переключением на повышенные частоты. Правда, это можно обойти. Добавьте строку `processor.ignore_ppc=1` в загрузку ядра или установите значение `/sys/module/processor/parameters/ignore_ppc` равное `1`.

* Некоторые комбинации драйверов ALSA и звуковых карт могут вызвать заикание звука во время переключения частот регулятором. Пока это можно решить только отключением регулятора масшабирования.
