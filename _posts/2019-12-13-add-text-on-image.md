---
title: "How to add text to image using Python"
categories:
  - Python
tags:
  - pillow
  - python
  - programming
---

Add text to image using PIL, Pillow Python

We can use ImageFont and ImageDraw to insert text to an image using Python

```python
from PIL import Image
from PIL import ImageFont
from PIL import ImageDraw 
img_sample = 'images/psili_ammos.jpeg'
img = Image.open(img_sample)
draw = ImageDraw.Draw(img)
# font = ImageFont.truetype(<font-file>, <font-size>)
# If a font is already installed in your system, you can 
# just give its name
font = ImageFont.truetype("arial.ttf", 24)
#or you can load default font
#font = ImageFont.load_default()
# x, y is the top-left coordinate
draw.text((10, 10),"Psili Ammos - Thassos",(255,255,255),font=font)
img.save('psili_ammos-out.jpg')
img.show()
```
![jpg]({{ site.url }}{{ site.baseurl }}/assets/images/psili_ammos-out.jpg)

The above code writes “Psili Ammos - Thassos” text to the existing image called psili_ammos-out.jpg

To create new blank violet image and then add the text to it, let change a little bit

```python
from PIL import Image
from PIL import ImageFont
from PIL import ImageDraw
window_height = 200
window_width = 300
img = Image.new(mode = "RGB", size = (window_width, window_height), color = (153, 153, 255) )
draw = ImageDraw.Draw(img)
font = ImageFont.truetype("arial.ttf", 36)
draw.text((50, 50), "Hello world!!!", font=font)
img.save('sample-out.jpg')
img.show()
```
![jpg]({{ site.url }}{{ site.baseurl }}/assets/images/sample-out.jpg)