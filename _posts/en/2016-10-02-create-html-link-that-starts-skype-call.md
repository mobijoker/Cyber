---
title: Create HTML link that starts a Skype call
ref: create-html-link-that-starts-skype-call
permalink: /web/create-html-link-that-starts-skype-call.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - skype
  - call
  - call me
  - chat me
  - skype button
  - skype link
  - skype call
  - skype chat

---

![thumb](/images/thumbnail/skype-call.png)
Nowadays most of the people use Skype, but not everyone knows that we can use an HTML link to launch Skype calls from your web browser or emails. Today I'll show how to add a Skype "Call Me" button to your website or blog and let people get in touch with just the click of a button. Whether they're on a computer or mobile, they will get through with a voice call or an instant message.

<br>

Here is an examples:

<table style="width:100%">
  <tr>
    <th><a href="skype:echo123?call"><img src="/images/call.png"></a></th>
    <th><a href="skype:echo123?call">Call Me</a></th> 
    <th><a href="skype:echo123?chat">Chat with Me</a></th>
  </tr>
</table>
<br>

The examples above will use the demo user of Skype (`echo123`) – which will record a call and play it back or ping back the typed in chat messages.


## Link with Phone number

To create an HTML link that starts a Skype call to phone number use the following example where you need to replace the `1234567890` with a valid phone number.

```
<a href="skype:+1234567890?call">Call Me</a>
```

The optional flag is `call` – to force Skype to call.

Also you can use the another method that is more universal:

```
<a href="callto://+1234567890">Call Me</a>
```


## Link with Skype Username

Firstly you need to know your Skype username. You can find it by [this](https://support.skype.com/en/faq/FA10858/what-s-my-skype-name) Skype tutorial.

Then, to create an HTML link that starts a Skype call to Skype user use the following example where you need to replace the `username` with your Skype username that you finded before.

```
<a href="skype:username?call">Call Me</a>
```

The optional flag is `call` – to force Skype to call.

Instead of the text "Call Me" you can use an image:

```
<a href="skype:username?call"><img src="/images/call.png"></a>
```

You can choose icons to your taste on [iconfinder.com](https://www.iconfinder.com/search/?q=call&ref=ArthurGareginyan).

Also we have a several options to add after the `?` in the `href` attribute. The syntaxis is `skype:username` and optional flags. See the examples below to see the usage.


### See info about a Skype user

The optional flag is `userinfo`. Example:

```
skype:username?userinfo
```

### Add a Skype user to address book

The optional flag is `add`. Example:

```
skype:username?add
```

### Send a message to chat

The optional flag is `chat`. Example:

```
skype:username?chat
```

### Send a VoiceMail to a Skype user

The optional flag is `voicemail`. Example:

```
skype:username?voicemail
```

### Create a Skype conference call with multiple users

The optional flag is `call`. By separating with semicolons list the users that you want to connect. Example:

```
skype:username1;username2?call
```

### Create a conference chat with multiple users

The optional flag is `chat`. By separating with semicolons list the users that you want to connect. Example:

```
skype:username1;username2?chat
```


## Tips & Warnings

* Users must have Skype already installed on their devices in order to the link worked.
* When testing your own link, it will probably say, `You cannot call yourself!` Don't worry, it will work for everyone else.
* You can get officially generated Skype button [here](https://www.skype.com/en/developer/create-contactme-buttons/). Skype offers a button that shows your current status.
