---
title: "Python - Blending Two Images using OpenCV"
img: "/assets/images/blended.png"
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

```

#### Resizing Images

In this step, we will resize the images that we want to blend. This step can also be called preprocessing the images. We are resizing the images to make sure they are in the same size. The same size rule is required for the blend function to work properly. Otherwise, it will return an error message.

```python

dim = (1200, 800) 
resized_bg = cv2.resize(bg, dim, interpolation = cv2.INTER_AREA) 
resized_fg = cv2.resize(fg, dim, interpolation = cv2.INTER_AREA)

```
Now, our images are in the same size. We can move to the next step, where we will start the blending process. In other words, the fun part of this whole article.

#### Blending Images

Thanks to OpenCV, we can do it in one line of code. The function that will do the blending for us is called addWeighted. It has 5 parameters, which can be listed as: image source 1, src1 weight, image source 2, src2 weight, gamma. The weight of each image has to be a value less than 1. Here is the blend equation:

> blend = (image scr1)*(src1 weight) + (image scr2)*(src2 weight) + gamma

That’s the mathematics of the function. Let’s see in action:


```python

blend = cv2.addWeighted(resized_bg, 0.5, resized_fg, 0.8, 0.0)

```

#### Exporting the Result

Now, let’s export the final work by using the imwrite method. Here is the line to save the image as a new image file in the folder.


```python

cv2.imwrite('blended.png', blend)

```

![png]({{ site.url }}{{ site.baseurl }}/assets/images/blended.png)