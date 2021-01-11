---
title: "BUILDING A DIGITAL CLOCK USING PYTHON"
header:
  image: /assets/images/images/digital_clock.png
  og_image: /assets/images/images/digital_clock.png
categories:
  - Python
tags:
  - Tkinter
---


#### 1. Python
Python is a general-purpose programming language that is becoming ever more popular for analyzing data. Python also lets you work quickly and integrate systems more effectively. Companies from all around the world are utilizing Python to gather bits of knowledge from their data. The official Python page if you want to learn more.

#### 2. Import Libraries
We will use two libraries in this project. And both of them come with Python, which means we don’t have to install them. These kind of libraries is called Python built-in packages.

The main package we will use is Tkinter. You can learn more about Tkinter from here, the official documentation page.

So for this step, all we need to do is to import them to our program:



```python
from tkinter import Label, Tk 
import time
```

#### 3. Designing the Application Window
In this step, we will first define the window panel using Tkinter package. And after that, we will define the text design that we want to use for the digital clock.

#### 4.Define the Window
As mentioned earlier, we will use Tkinter package. Tkinter is can be defined as Tk. And after defining it, we will customize it.




```python
app_window = Tk()
app_window.title("Python Digital Clock")
app_window.geometry("350x150")
app_window.resizable(0,0)
```




    ''



Perfect, our application window is ready! Now, let’s work on the clock design.

#### The Label Design
The cool step of the program is this one. Because you can put your own preferences into the design. This step will make your work different from others. If you love designing things, it’s time to show off your skills.

There are four elements that we will customize:

- The font of the digital numbers.
- The background color of our digital clock.
- The color of the digital numbers, make sure it is not the same color as your background. 😉
- The border width of the text.
- Here are the values that I used for my design:


```python
text_font = ("Boulder", 68, 'bold')
background = "#f2e750"
foreground = "#363529"
border_width = 25
```

For colors, feel free to use RGB values or hex values. In my case, I used the hex values of the colors. I use google’s color picker that is available on the browser. Just search “Color picker” on google search. And you will see it.

Now, let’s combine the elements and define our label. Label function is the text that will show our time.


```python
label = Label(app_window, font=text_font, bg=background, fg=foreground, bd=border_width)
label.grid(row=0, column=1)
```

#### 4. Digital Clock Function
If we are working on an application project, functions are the best way to make things work. Functions are also great because they make the program more structured and easier to understand. Alright, let’s define our digital clock function then:


```python
def digital_clock():
    time_live = time.strftime("%H:%M:%S")
    label.config(text=time_live)
    label.after(200, digital_clock)
```

Understanding the code:

In the first line, we are getting real-time using the time package. And we are also defining the format that we want it to be. Since we are designing a digital clock, “hour, minutes, seconds” will be a nice format to go with.
In the second line, we are just assigning the real-time to the label method. This way the digital time will be updated.
And lastly, we are calling the function again so that the digital clock is showing the live time. This way every 200 milliseconds the time is getting updated. In programming, this is called a recursion loop. Calling the same function, inside the function. Feels like inceptions, isn’t that cool? 

#### 5. Run the Application
Great! You made it until this step, which is the final step of our application project. As you know functions will not run unless you call them. To trigger the application, we will call the function. Let’s run the application:


```python
digital_clock()
app_window.mainloop()
```

![png]({{ site.url }}{{ site.baseurl }}/assets/images/digital_clock.png)
