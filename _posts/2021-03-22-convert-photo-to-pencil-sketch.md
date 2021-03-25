---
title: "Convert A Photo To Pencil Sketch Using Python"
img: "blended.png"
categories:
  - Python
tags:
  - opencv
---

In this article, I will show you how to convert an image to a pencil sketch using the Python programming language in just 5 lines of code! Python is a general-purpose programming language that was created in the late 1980s and has seen significant growth in popularity from big tech companies and communities over the years.
One of the reasons for its popularity growth is its ease of use and simplicity. Just think that we are about to transform an image in just 5 lines of code !!
Actually, it could be less.

Quick Steps:
1. Convert the RGB colour image to grayscale.
2. Invert the grayscale image to get a negative.
3. Apply a Gaussian blur to the negative from step 2.
4. Blend the grayscale image from step 1 with the blurred negative from step 3

![jpg]({{ site.url }}{{ site.baseurl }}/assets/images/background.jpg)

![png]({{ site.url }}{{ site.baseurl }}/assets/images/foreground.png)

Step 1: Find an image that we want to convert into a pencil sketch. I am going to use the image of a Mickey Mouse

```python
import cv2
image = cv2.imread("input/miki_mouse.png")

```

Step 2: Read in the Red, Blue, Green (RBG) image and then convert it to a grayscale image. This effectively makes the image a classic “black and white” photo. This will be our “greyscale image”.

```python
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
cv2.imwrite("output/gray.png", gray_image)

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