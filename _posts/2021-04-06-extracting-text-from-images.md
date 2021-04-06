---
title: "Extract text with OCR in python using pytesseract"
img: "ocr.png"
categories:
  - Python
tags:
  - OCR, pytesseract
---

What is OCR?
Optical Character Recognition(OCR) is the process of electronically extracting text from images or any documents like PDF and reusing it in a variety of ways such as full text searches.
In this blog, we will see, how to use ‘Python-tesseract’, an OCR tool for python.

pytesseract:
It will recognize and read the text present in images. It can read all image types — png, jpeg, gif, tiff, bmp etc. It’s widely used to process everything from scanned documents.



Step 1: I am going to use the folowwing image to extract text 

![png]({{ site.url }}{{ site.baseurl }}/assets/images/mostovi.png)

```python
# importing modules
import csv
import cv2
import pytesseract

prefix = 'mostovi'
# eng, srp, srp_latn ...
lang = 'srp_latn'
# reading image using opencv
image = cv2.imread("input/"+prefix+".png")

# converting image into gray scale image
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# converting it to binary image by Thresholding
# this step is require if you have colored image because if you skip this part
# then tesseract won't able to detect text correctly and this will give incorrect result

threshold_img = cv2.threshold(
    gray_image, 0, 255, cv2.THRESH_BINARY | cv2.THRESH_OTSU)[1]

# configuring parameters for tesseract

custom_config = r'--oem 3 --psm 6'

# now feeding image to tesseract

details = pytesseract.image_to_data(
    threshold_img, output_type=pytesseract.Output.DICT, config=custom_config, lang=lang)

# print(details.keys())

```
Step 2: Read in the Red, Blue, Green (RBG) image and then convert it to a grayscale image. This effectively makes the image a classic “black and white” photo. This will be our “greyscale image”.

```python
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
cv2.imwrite("output/gray.png", gray_image)

```

If you print the details, these are the dictionary keys that will contain relevant details:
dict_keys(['level', 'page_num', 'block_num', 'par_num', 'line_num', 'word_num', 'left', 'top', 'width',
	'height', 'conf', 'text'])

The above dictionary has the information of your input image such as its detected text region,
position information, height, width, confidence score, etc.
Now, draw the bounding box on your original image using the above dictionary to find out
how accurately Tesseract works as a text scanner to detect the text region. Follow the code given below:

In this step we consider only those images whose confidence score is greater than 30.
Get this value by manually looking at the dictionary’s text file details and confidence score.
After this, verify that all the text results are correct even if their confidence score is between 30-40.
You need to verify this because images have a mixture of digits, other characters, and text.
And it is not specified to Tesseract that a field has only text or only digits.
Provide the whole document as it is to Tesseract and wait for it to show the results based on the value
whether it belongs to text or digits.

```python

total_boxes = len(details['text'])  

for sequence_number in range(total_boxes):  

  if int(details['conf'][sequence_number]) > 30: 

    (x, y, w, h) = (details['left'][sequence_number], details['top'][sequence_number],
                    details['width'][sequence_number],  details['height'][sequence_number]) 

    threshold_img = cv2.rectangle(
        image, (x, y), (x + w, y + h), (0, 255, 0), 2) 

# cv2.imshow('captured text', threshold_img) 
cv2.imwrite('OCR/'+'captured-'+prefix+'.png', threshold_img)

```

![png]({{ site.url }}{{ site.baseurl }}/assets/images/captured-mostovi.png)

Now that you have an image with the bounding box, you can move on to the next part which is to arrange
the captured text into a file with formatting to easily track the values.

Note: Here, I have written the code based on the current image format and output from Tesseract.
If you are using some other image format then you need to write the code according to that image format.

The code given below is to arrange the resulted text into a format as per the current image:

```python
parse_text = [] 

word_list = [] 

last_word = ''

for word in details['text']: 

  if word != '': 
    print(word)

    word_list.append(word) 

    last_word = word

  if (last_word != '' and word == '') or (word == details['text'][-1]): 

    parse_text.append(word_list) 

    word_list = [] 

with open('OCR/result_'+prefix+'_text.txt',  'w', newline="") as file:
  csv.writer(file, delimiter=" ").writerows(parse_text)
 
```

