---
id: 647
lang: en
ref: terminal-tweaks-for-os-x-lion-10-7
title: Terminal Tweaks for OS X Lion 10.7
date: 2015-06-24T17:20:52+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=647
permalink: /mac-os/terminal-tweaks-for-os-x-lion-10-7.html
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
Given time, the performance of any computer will tend to degrade – even Macs. In this post I'll show you tweaks that I use on my MacBook White with Mac OS X 10.7 Lion.


### Disable Dashboard

It is possible to completely disable OS X Dashboard. This could save some memory and cpu resources.

Use the following command:

```
defaults write com.apple.dashboard mcx-disabled -boolean true ; killall Dock
```

You can reactivate OS X Dashboard by using this command:

```
defaults write com.apple.dashboard mcx-disabled -boolean false ; killall Dock
```


### Keep Quick Look windows in front

When viewing a file with QuickLook it will appear in the foreground of the screen. When you select a different window, QuickLook will go to the background. It’s possible to keep the QuickLook windows in front.

Terminal command:

```
defaults write com.apple.Finder QLHidePanelOnDeactivate 0 ; killall Finder
```

Revert the change with:

```
defaults write com.apple.Finder  1 ; killall Finder
```


### Disable fade effects of Launchpad

Launchpad shows a fade effect anytime it is opened or closed. If you want to access Launchpad a little bit faster, it’s possible to disable the fade effects.

Terminal commands:

```
defaults write com.apple.dock springboard-show-duration -int 0
defaults write com.apple.dock springboard-hide-duration -int 0
killall Dock
```

Re-enable launchpad fading effect:

```
defaults delete com.apple.dock springboard-show-duration
defaults delete com.apple.dock springboard-hide-duration
killall Dock
```


### Disable window animations in Finder

Disable all window animations and the animation when opening the info window in Finder. 

Use the following OS X Terminal command:

```
defaults write com.apple.finder DisableAllAnimations -bool true
```

To restore the animations in OS X Finder:

```
defaults write com.apple.finder DisableAllAnimations -bool false
```


### Disable the new window animation in Mac OS X

Turn off the new window animation in Mac OS X 10.7 and higher, new windows will appear instantly without delay.

Terminal command:

```
defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool false
```

Relaunch any currently running apps or reboot your Mac to have the changes take effect.

To restore the new window animation:

```
defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool true
```


### Enable the 2D Dock

If the 3D Dock isn’t your taste, you can switch to the 2D visual implementation.

Terminal command:

```
defaults write com.apple.dock no-glass -boolean YES ; killall Dock
```

Revert the change with:

```
defaults write com.apple.dock no-glass -boolean NO ; killall Dock
```


### Enable AirDrop in a wired network and old Macs

Enable the AirDrop in a wired network even when your Mac is not supported:

```
defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool true ; killall Finder
```

After restarting the Finder, Airdrop will appear in Finder’s navigation bar.

Revert the change with:

```
defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool false ; killall Finder
```
