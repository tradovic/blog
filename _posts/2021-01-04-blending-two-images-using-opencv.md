---
title: "Python - Blending Two Images using OpenCV"
categories:
  - Python
tags:
  - opencv
---

In this article, I will show you how to create nice looking custom designs using Python. There are many designing tools out there, but our goal is to create a beautiful design without using any of those software in this project. After working on this project, you will also have an idea on how to work with the OpenCV package. It is a great skill to have, especially if you like computer vision. You can follow a similar structure when working on similar OpenCV projects.

I love art and doing design work, and in this project, I wanted to combine my passion and programming. This is actually one of the biggest reasons I enjoy programming; it gives me the opportunity to work in very different areas depending on the interest. I see programming like a pencil and the text editor as blank paper. It all starts with your imagination skills. The rest comes as you start writing the code. Python makes this process much smoother and more fun. Enough with the introduction. Let’s get started!

In this exercise, I will blend a text image with a nice background image. Let me show you the two images that I will be working on:

![jpg]({{ site.url }}{{ site.baseurl }}/assets/images/background.jpg)

![png]({{ site.url }}{{ site.baseurl }}/assets/images/foreground.png)

```python
import cv2
bg = cv2.imread('images/background.jpg', cv2.IMREAD_COLOR) 
fg = cv2.imread('images/foreground.png', cv2.IMREAD_COLOR)

dim = (1200, 800) 
resized_bg = cv2.resize(bg, dim, interpolation = cv2.INTER_AREA) 
resized_fg = cv2.resize(fg, dim, interpolation = cv2.INTER_AREA)
blend = cv2.addWeighted(resized_bg, 0.5, resized_fg, 0.8, 0.0)
cv2.imwrite('blended.png', blend)
```

![png]({{ site.url }}{{ site.baseurl }}/assets/images/blended.png)