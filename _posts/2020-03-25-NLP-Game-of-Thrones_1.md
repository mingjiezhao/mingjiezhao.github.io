---
layout: post
title: NLP Analysis for Game of Thones (1)
subtitle: Pre-processing, word frequency analysis and LDA
bigimg: /img/posts_imgs/post1-nlp/Game_of_Thrones_title_card.jpg
gh-repo: mingjiezhao/Game_of_thrones
gh-badge: [star, fork, follow]
tags: [NLP]
comments: true
---

## 1. Introduction
Many people around me are fans of Game of Thrones, and last summer I heard a lot of complaints about the show's ending. For whatever reason, my brain has had difficulty memorizing character names, especially when the relationships of characters are complicated. So I gave up watching the show after a few episodes. However, I think it would be very interesting to analyze the words of the characters. The show creates a fantastic world and I am curious to learn about the world through the characters's words (much faster than watching the whole show which includes 73 episodes), and that's the motiviation of this project. Hope you have fun reading it!

Since this analysis is a bit long, I figured it would be better to break it down to two posts. This is the first half of the analysis, including the data processing, word frequency analysis and LDA (topics model). The second post focus on sentiment analysis and word cloud analysis, as well as some conclusions. 

The analysis is made through R and the code is published in my [github](https://github.com/mingjiezhao/Game_of_thrones).

## 2. Methodology
In this project, I picked four characters with the most lines. You may be wondering by now about who are the most talkative ones in this show. Well, the answer will be provided below in the analysis. Since characters may speak around certain topics based on their character settings, I created LDA (Latent Dirichlet Allocation) models of these 4 characters to see if there are main topics from what they said. I also performed sentiment analysis on their words to see how they feel about by living in the fantastic world. Data visualizations are created by multiple plots and some findings are provided at the end of the project.

## 3. Anslysis
### 1) Data preprocessing
Firstly, read in (a) dataset which was found on Github (json file provided by https://github.com/jeffreylancaster/game-of-thrones). The original dataset is a huge list of list and I manipulated the dataset to get a list of the characters and a new dataframe to count for numbers of sentence for each character. We can see that the average number of sentences in the show across all the characters is 181.5, while the most talktaive character said 1704 sentences. However, there are a lot of characters who only said one sentence in the show. And the 4 characters who are on my list of top 4 talktive ones are 
-Tyrion Lannister ![TL](https://upload.wikimedia.org/wikipedia/en/5/50/Tyrion_Lannister-Peter_Dinklage.jpg)
-Jon Snow ![JS](https://upload.wikimedia.org/wikipedia/en/3/30/Jon_Snow_Season_8.png)
- Daenerys Targaryen 
- Cersei Lannister. 

I hope this is not a surprising result to you if you are a fan, because what they've said would be very important here in my analysis below.


### 2) Word frequency analysis
To deal with the text data, I created a function to do data manipulation including removing punctuation, numbers and stopwords. I also did word stemming to remove affixes. Then I created a chart to show which words are used the most by these characters. It's interesting to see that these top words are highly correlated with each character's background. For example, Tyrion used "king" and "father" a lot, because he spent a lot of court business dealing with nobles. Also Tyrion lived in the shadow of his father Tywin Lannister for a long time, until he killed his own father. Daenerys liked to say "dragon" and "people", since she is the mother of three dragons, and is considered to be the "Mother of dragons". And  Cersei was the ruling queen of the seven kingdoms, until losing it to Dany. She married King Robert, and is mother of two kings. That may explain her favorite words like "king", "father" and "love".
![img1](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/post1-nlp/pic1.png?raw=true){: .center-block :}


### 3) LDA and topic model
Latent Dirichlet Allocation (LDA) is a widely used model in natural language processing (NLP) as an unsupervised learning method. In this project, I am trying to find 3 topics for each character. A function was written to perform the LDA modeling and a chart was plotted for the top 4 words in the 3 topics, to visualize the results and understand the topics that were extracted from these words.

It's interesting to see that some of the topics correlate closely with the show. For example, the third topic of Jon includes key words like "wall", "night" and "watch". This probably correlates with the story that Jon has served in the Night Watch, first as a personal steward of the then Lord Commander, and then became a Lord Commander of the Night Watch himself. The main duty of the Night Watch is to guard the Wall. Dany, undoubtedly associated with dragon, also has keywords in other languages, as she is ruling many people of different cultures and races. Another good example is the Topic 2 of Cersei include keywords like "love", "brother", and "daughter", while Cersei has a relationship and affair with her twin brother Jaime Lannister.
![img2](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/post1-nlp/pic2.png?raw=true){: .center-block :}
![img3](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/post1-nlp/pic3.png?raw=true){: .center-block :}




<!-- Here's a useless table:

| Number | Next number | Previous number |
| :------ |:--- | :--- |
| Five | Six | Four |
| Ten | Eleven | Nine |
| Seven | Eight | Six |
| Two | Three | One |


How about a yummy crepe?





## Boxes
You can add notification, warning and error boxes like this:

### Notification

{: .box-note}
**Note:** This is a notification box.

### Warning

{: .box-warning}
**Warning:** This is a warning box.

### Error

{: .box-error}
**Error:** This is an error box.
 -->