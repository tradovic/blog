---
title: "Convert A Photo To Pencil Sketch Using Python"
img: "Sketch.png"
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



Step 1: Find an image that we want to convert into a pencil sketch. I am going to use the image of a Mickey Mouse

```python
import cv2
image = cv2.imread("input/miki_mouse.png")

```
![png]({{ site.url }}{{ site.baseurl }}/assets/images/miki_mouse.png)

Step 2: Read in the Red, Blue, Green (RBG) image and then convert it to a grayscale image. This effectively makes the image a classic “black and white” photo. This will be our “greyscale image”.

```python
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
cv2.imwrite("output/gray.png", gray_image)

```
![png]({{ site.url }}{{ site.baseurl }}/assets/images/gray.png)

Step 3: We are going to invert the “grey scaled image” also known as getting the image negative, this will be our “inverted greyscale image”. Inversion can be used to enhance details.

```python

inverted_image = 255 - gray_image
cv2.imwrite("output/inv.png", inverted_image)

```

![png]({{ site.url }}{{ site.baseurl }}/assets/images/inv.png)

Step 4: Use a Gaussian function to blur the image. In image processing, a Gaussian blur (also known as Gaussian smoothing) is the result of blurring an image by a Gaussian function.

```python

blurred = cv2.GaussianBlur(inverted_image, (21, 21), 0)
cv2.imwrite("output/blur.png", blurred)
 
```

![png]({{ site.url }}{{ site.baseurl }}/assets/images/blur.png)

Step 5: Invert the newly created “blurred image”, this will be called the “inverted blurred image”.


```python

inverted_blurred = 255 - blurred
cv2.imwrite("output/invblur.png", inverted_blurred)

```
![png]({{ site.url }}{{ site.baseurl }}/assets/images/invblur.png)

Step 5: Now we are going to create the pencil sketch image by blending the “greyscale image” with the “inverted blurred image”. This can be done by dividing the “grayscale image” by the “inverted blurred image”. Since images are just arrays we can easily do this in programming by using the divide function from the cv2 library.

```python

pencil_sketch = cv2.divide(gray_image, inverted_blurred, scale=256.0)
cv2.imwrite("output/Sketch.png", pencil_sketch)

```

![png]({{ site.url }}{{ site.baseurl }}/assets/images/Sketch.png)