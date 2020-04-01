---
layout: post
title: NLP Analysis for Game of Thones (2)
subtitle: Sentiment analysis and word cloud
gh-repo: mingjiezhao/Game_of_thrones
<!-- gh-badge: [star, fork, follow] -->
tags: [NLP]
comments: true
bigimg:(https://upload.wikimedia.org/wikipedia/en/d/d8/Game_of_Thrones_title_card.jpg)
---

## 1. Overview
Many people around me are fans of Game of Thrones, and last summer I heard a lot of complaints about the show's ending. I think it would be very interesting to analyze the words of the characters.  

Since this analysis is a bit long, I figured it would be better to break it down to two posts. This is the second half of the analysis, focusing on sentiment analysis and word cloud analysis, as well as some conclusions. 

The analysis is made through R and the code is published in my [github](https://github.com/mingjiezhao/Game_of_thrones).

## 2. Sentiment analysis

It is also insightful to perform setiment analysis to check emotions within the lines. Two plots were made for each character. The first plot shows the top words contributing the most to positive and negative emotions, and the second plot shows the top 15 emotional words that contribute to sentiment. It is interesting to see that the word "love" is the top positive word appearred in the analysis results for all 4 characters. Additionally, it is worth noticing that in the second plot (Contribution to sentiment) for all four main characters, there are more negtive words contributing to sentiment than positive words, indicating a negative attitude in lines for the four characters.
![img4](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/post1-nlp/pic4.png?raw=true){: .center-block :}
![img5](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/post1-nlp/pic5.png?raw=true){: .center-block :}
![img6](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/post1-nlp/pic6.png?raw=true){: .center-block :}
![img7](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/post1-nlp/pic7.png?raw=true){: .center-block :}

## 3. Word cloud
Last but not least, I created a word cloud for each character to visualize the emotional words in lines. We can see that on the negative side, "kill" and "die" are really eyes-catching, while "love" and "grace" pop up in the positive side.
Tyrion Lannister
![img8](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/post1-nlp/pic8.png?raw=true){: .center-block :}
Jon Snow
![img9](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/post1-nlp/pic9.png?raw=true){: .center-block :}
Daenerys Targaryen
![img10](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/post1-nlp/pic10.png?raw=true){: .center-block :}
Cersei Lannister
![img11](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/post1-nlp/pic11.png?raw=true){: .center-block :}

## 4. Conclusions
In this project, I used 5 ways to analyze the lines from Game of Thrones with NLP techniques. As a summary the LDA and topic model do a good job in terms of representing the stories of each character. The sentiment analyses provide insights about the emotions of these characters. It is interesting to see that most of the results correspond to the background of the chatacters. This show mostly provides the audience with negative emotions, but I am happy to see that love is the most used positive word.

## Reference
Julia Silge and David Robinson,"Text Mining with R"



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