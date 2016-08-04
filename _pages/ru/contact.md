---
title: Контакты
lang: ru
ref: contact
order: 2
date: 2015-09-11T17:44:11+00:00
author: Arthur Gareginyan
layout: page
permalink: /ru/contact.html
redirect_from: /ru/contacts.html

---

<form id="contact-form" action="http://formspree.io/arthurgareginyan@gmail.com" method="POST">

<div class="field-left">

    <div class="form-title">Name:</div>
    <input type="text" name="name" placeholder="Enter your name" class="form-field">

    <div class="form-title">Email:</div>
    <input type="email" name="_replyto" placeholder="Enter your email" class="form-field">

</div>
<div class="field-right">

    <div class="form-title">Subject :</div>
    <input type="email" name="subject" placeholder="Enter the subject" class="form-field">

    <div class="form-title">Website <span style="color:#aaaaaa">(If applicable)</span>:</div>
    <input type="email" name="website" placeholder="Enter the URL" class="form-field">

</div>

    <div class="form-title">Message:</div>
    <textarea name="message" rows="10" placeholder="Enter your message" class="form-field form-message"></textarea>

    <input type="hidden" name="_subject" value="Website contact" />
    <input type="hidden" name="_next" value="//www.mycyberuniverse.com/contact-thanks.html" />
    <input type="text" name="_gotcha" style="display:none">

    <div class="buttons-container">
       <input type="submit" value="Send" class="buttons">
    </div>

</form>

<style>
#contact-form {
   font-family: Georgia, Palatino, Palatino Linotype, Times, Times New Roman, serif;
   font-size: 16px;
   width: 100%;
}

.field-left {
   width: 50%;
   display: inline-block;
   float: left;
}

.field-right {
   width: 50%;
   display: inline-block;
}

.form-title {
   margin-bottom:10px;
   color: #fff;
   text-shadow: #fdf2e4 0 1px 0;
}

.form-field {
   border: 1px solid #a39584;
   background: #f3f3f3;
   -webkit-border-radius: 4px;
   -moz-border-radius: 4px;
   border-radius: 4px;
   color: #C4C4C4;
   -webkit-box-shadow: rgba(255,255,255,0.4) 0 1px 0, inset rgba(000,000,000,0.7) 0 0px 0px;
   -moz-box-shadow: rgba(255,255,255,0.4) 0 1px 0, inset rgba(000,000,000,0.7) 0 0px 0px;
   box-shadow: rgba(255,255,255,0.4) 0 1px 0, inset rgba(000,000,000,0.7) 0 0px 0px;
   padding: 8px;
   margin-bottom: 20px;
   width: 90%;
}
.form-field:focus {
   background: #fff;
   color: #725129;
}

.form-message {
   width: 95%;
}

.buttons-container {
   margin: 8px 0;
   //text-align: center;
}

.buttons {
	-moz-box-shadow:inset 0px 1px 0px 0px #ffffff;
	-webkit-box-shadow:inset 0px 1px 0px 0px #ffffff;
	box-shadow:inset 0px 1px 0px 0px #ffffff;
	background:-webkit-gradient(linear, left top, left bottom, color-stop(0.05, #f9f9f9), color-stop(1, #e9e9e9));
	background:-moz-linear-gradient(top, #f9f9f9 5%, #e9e9e9 100%);
	background:-webkit-linear-gradient(top, #f9f9f9 5%, #e9e9e9 100%);
	background:-o-linear-gradient(top, #f9f9f9 5%, #e9e9e9 100%);
	background:-ms-linear-gradient(top, #f9f9f9 5%, #e9e9e9 100%);
	background:linear-gradient(to bottom, #f9f9f9 5%, #e9e9e9 100%);
	filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#f9f9f9', endColorstr='#e9e9e9',GradientType=0);
	background-color:#f9f9f9;
	-moz-border-radius:6px;
	-webkit-border-radius:6px;
	border-radius:6px;
	border:1px solid #dcdcdc;
	display:inline-block;
	cursor:pointer;
	color:#666666;
	font-family:Arial;
	font-size:15px;
	font-weight:bold;
	padding:6px 24px;
	text-decoration:none;
	text-shadow:0px 1px 0px #ffffff;
}
.buttons:hover {
	background:-webkit-gradient(linear, left top, left bottom, color-stop(0.05, #e9e9e9), color-stop(1, #f9f9f9));
	background:-moz-linear-gradient(top, #e9e9e9 5%, #f9f9f9 100%);
	background:-webkit-linear-gradient(top, #e9e9e9 5%, #f9f9f9 100%);
	background:-o-linear-gradient(top, #e9e9e9 5%, #f9f9f9 100%);
	background:-ms-linear-gradient(top, #e9e9e9 5%, #f9f9f9 100%);
	background:linear-gradient(to bottom, #e9e9e9 5%, #f9f9f9 100%);
	filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#e9e9e9', endColorstr='#f9f9f9',GradientType=0);
	background-color:#e9e9e9;
}
.buttons:active {
	position:relative;
	top:1px;
}
</style>
