---
lang: ru
ref: terminal-tweaks-for-os-x-lion-10-7
title: Терминальные Твики OS X Lion 10.7
date: 2015-06-24T17:20:52+00:00
author: Arthur Gareginyan
layout: post
permalink: /ru/mac-os/terminal-tweaks-for-os-x-lion-10-7.html
switch_like_status:
  - 1
categories:
  - Mac OS
tags:
  - 10.7
  - 10.7.5
  - console
  - mac
  - mac os
  - os
  - os lion
  - os x
  - speed up
  - terminal
  - tune up
  - tuneup
  - tweak

---

![thumb](/images/OS-X-Tweaks-150x150.png)
Со временем, производительность любого компьютера ухудшаеться – даже Mac. В этом посте Я покажу вам твики которые Я использую на своём MacBook White с Mac OS X Lion 10.7.


### Отключение Dashboard'а

Можно полностью отключить OS X Dashboard. Это может сохранить немного памяти и ресурсы процессора.

Используйте следующую команду:

```sh
defaults write com.apple.dashboard mcx-disabled -boolean true ; killall Dock
```

Вы можете повторно активировать OS X Dashboard с помощью следующей команды:

```sh
defaults write com.apple.dashboard mcx-disabled -boolean false ; killall Dock
```


### Держать Quick Look окна на переднем плане

При просмотре файла с помощью QuickLook, он будет отображаться на переднем плане экрана, но при выборе другого окна, QuickLook уходит на задний план. Можно сделать так, чтобы QuickLook окна держались на переднем плане постоянно.

```sh
defaults write com.apple.Finder QLHidePanelOnDeactivate 0 ; killall Finder
```

Для отмены изменений:

```sh
defaults write com.apple.Finder  1 ; killall Finder
```


### Отключение эффекта при закрытии Launchpad'а

Launchpad показывает эффект затухания во время открытия или закрытия. Отключение эффекта ускорит доступ к Launchpad.

```sh
defaults write com.apple.dock springboard-show-duration -int 0
defaults write com.apple.dock springboard-hide-duration -int 0
killall Dock
```

Для отмены изменений:

```sh
defaults delete com.apple.dock springboard-show-duration
defaults delete com.apple.dock springboard-hide-duration
killall Dock
```


### Отключение анимации окон в Finder

Отключить всю анимацию окон и анимацию при открытии окна информация в Finder. 

```sh
defaults write com.apple.finder DisableAllAnimations -bool true
```

Для отмены изменений:

```sh
defaults write com.apple.finder DisableAllAnimations -bool false
```


### Отключение новой анимации окон в Mac OS X

Если отключить новую анимацию окон в Mac OS X 10.7 и выше, то новые окна будут появляться мгновенно, без задержки.

```sh
defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool false
```

Перезапустите все запущенные приложения или перезагрузите ваш Mac для того, чтобы изменения вступили в силу.

Для отмены изменений:

```sh
defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool true
```


### Включение 2D Dock

Если 3D Dock не в вашем вкусе, то вы можете переключится на 2D.

```sh
defaults write com.apple.dock no-glass -boolean YES ; killall Dock
```

Для отмены изменений:

```sh
defaults write com.apple.dock no-glass -boolean NO ; killall Dock
```


### Включение AirDrop в проводной сети и на старых Mac

Можно включить AirDrop в проводной сети и на неподдерживаемых Mac:

```sh
defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool true ; killall Finder
```

После перезагрузки Finder, Airdrop будет отображаться в навигационной панели Finder'а.

Для отмены изменений:

```sh
defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool false ; killall Finder
```
