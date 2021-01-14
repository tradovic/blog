---
title: "Create Word Cloud from Text"
img: "output_13_0.png"
categories:
  - Python
tags:
  - NLP
---


### Create a Word Cloud or Tag Cloud in Python

###### Python tutorial for creating a Word Cloud from any given text.

A Word Cloud or a Tag Cloud is a data visualization technique where words from a given text are displayed in a chart, with the more important words being written with bigger, bold fonts, while less important words are displayed with smaller, thinner fonts or not displayed at all.


Lots of Natural Language Processing projects can benefit from the use of Word Clouds because this tool can give you a quick glance at what the text you are analyzing is about and because it can help you, as a developer, or your audience, to understand the context of your dataset.

In today's project we are going to download the text from a Wikipedia page, and then generate a word cloud and play with it for a bit - changing colors, removing stopwords and saving the wordcloud to a file.

We need to install a few packages before we begin.
pip3 install wikipedia
pip3 install wordcloud
We will also need matplotlib, but this is installed automatically by wordcloud, if you don't have on your local.

Since we've installed our packages, we might as well import them into our project.


```
import wikipedia
from wordcloud import WordCloud, STOPWORDS
import matplotlib.pyplot as plt
```

Now we are going to use the wikipedia package to download the text content. All we need for this is to provide the title of the page. We are going to fetch the text for the Natural Language Processing page on Wikipedia.


```
page = wikipedia.page("Natural Language Processing")
text = page.content
```

Next we can use this text to generate and display the word cloud.


```
def plot_cloud(wordcloud):
  plt.figure(figsize=(8, 8), facecolor=None)
  plt.imshow(wordcloud, interpolation="bilinear")
  plt.axis("off")
  plt.tight_layout(pad=0)
  plt.show()
```


```
wordcloud = WordCloud().generate(text)
plot_cloud(wordcloud)
```


![png](output_13_0.png)


Understanding this word cloud is very intuitive, you can observe that these words are very common when we read something about Natural Language Processing. Let's see another example, this time with the article about Machine Learning.

We can do lots of personalization on a word cloud: changing fonts, changing colors and the way they are displayed. For more options, you can always check the documentation of the package.

To demonstrate how easy it is, let's at least change the background color. For that, we only need to add a new parameter to the WordCloud constructor.



```
ml_page = wikipedia.page("MachineLearning")
ml_text = ml_page.content
cloud = WordCloud(background_color='white').generate(ml_text)
plot_cloud(cloud)
```


![png](output_16_0.png)


###### Removing stopwords from a word cloud

Stop words are words that are very frequently used in a given language and add absolutely no meaning to the text(because other texts will also contain these words, a stop word does not tell us anything about our text corpus).

The wordcloud package already removes the most common stopwords for us. But if you think that your text corpus has some stop words that are not removed, you can always append new words that will be removed. Here's how:


```
# Additional import here
from wordcloud import WordCloud, STOPWORDS
###########
stopwords = set(STOPWORDS)
stopwords.update(["stopword1", "stopword2"])
cloud = WordCloud(stopwords=stopwords, background_color='white').generate(text)
```

###### Saving our word cloud to a file

We can also save our word cloud with a single line of code.


```
cloud.to_file("wordcloud.png")
```




    <wordcloud.wordcloud.WordCloud at 0x11a484748>



That was quick! We've generated our word cloud in very few lines of code and we can use this to better understand our data whenever we work on some Natural Language Processing project.


```

```
