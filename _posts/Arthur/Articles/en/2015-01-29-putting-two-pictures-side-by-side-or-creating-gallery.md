---
lang: en
ref: putting-two-pictures-side-by-side-or-creating-gallery
title: Putting two pictures side by side or creating gallery
date: 2015-01-29
author: Arthur Gareginyan
layout: post
permalink: /web/putting-two-pictures-side-by-side-or-creating-gallery.html
categories:
  - Web
tags:
  - blogger
  - cms
  - gallery
  - image
  - photo
  - picture
  - side by side
  - table
  - wordpress

---

![thumb](/images/thumbnail/Preview-icon.png)
When you have many images that you want to include in a blog post, it is important to place them compactly. This way, the reader won’t have to scroll down forever and ever to see your images. Here’s a simple solution to do that.


<br><br>

All you need is a table. In a table you can place multiple images on the grid. You can use two, three or more columns.


<br>
**Step 1.** Insert the table code to place where you need to put two pictures on the same line.

```
<table>
<tbody>
	<tr>
		<td>Photo 1</td>
		<td>Photo 2</td>
	</tr>
</tbody>
</table>
```

Note: Replace the `Photo 1` and `Photo 2` with links to your images.

If you have more then two images then, repeat part of the table code like following:

```
<table>
<tbody>
	<tr>
		<td>Photo 1.1</td>
		<td>Photo 1.2</td>
	</tr>
	<tr>
		<td>Photo 2.1</td>
		<td>Photo 2.2</td>
	</tr>
	<tr>
		<td>Photo 3.1</td>
		<td>Photo 3.2</td>
	</tr>
</tbody>
</table>
```

Note: Replace the `Photo *` with links to your images.


<br>
**Step 2.** Insert your images into boxes instead of text “Photo 1” and “Photo 2” etc.

Example:
<table>
<tbody>
	<tr>
		<td>Photo 1.1</td>
		<td>Photo 1.2</td>
	</tr>
	<tr>
		<td>Photo 2.1</td>
		<td>Photo 2.2</td>
	</tr>
	<tr>
		<td>Photo 3.1</td>
		<td>Photo 3.2</td>
	</tr>
</tbody>
</table>


<br>
**P.S.**
This solution is works in Blogger, WordPress and other CMS.
