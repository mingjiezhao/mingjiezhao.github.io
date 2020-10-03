---
layout: post
title: Did your friend cheat in the drinking game for the 1st Presidential Debate 2020?
subtitle: An Exploration with Python 
tags: [2020 Election]
comments: true
---
I am wondering how many people played or at least saw pics of the “drinking game” designed for the first presidential debate of 2020. As a person who has extremely low alcohol tolerance (2 beers), I know I would never win this, or any drinking game. However, it did reduce any entertainment I got from the super debate show. I am not sure if you could recognize every single key work for shots when watching the debate alive, I guess people would cheat purposely (too many keywords were hit) or unintentionally (when they talk all together, could you really tell who said what?).

Well, no worries. If you feel your friends and/or families ever cheated in the drinking game, or you are not sure how much alcohol you need to purchase for the next presidential debate on Oct. 15 (well, I mean if there will be one), I am here to provide you with some suggestions on how many shots they should have taken and how many bottles you need (based on data analysis). Show them this post and ask them to make it up if they cheated in drinking!

I am using this drinking game from the [internet](https://www.barstoolsports.com/blog/2916035/hard-factor-presidential-debate-watch-party-with-pft-commenter-and-cousin-mike)
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/first_debate/drinking-game-debate.jpeg?raw=true){: .center-block :}
Hint: Though I don’t know who won the debate, I am pretty sure most people would lose in the drinking game, or got too drunk to survive the whole show.

This analysis is based on the data provided by [Kaggle](https://www.kaggle.com/theogoe/first-pres-debate-2020). This dataset records sentences from each speaker (Trump, Biden and Wallce), time spoken, words per minute, and number of words. First, I made some simple pie charts to figure out who was the most talkative guy. It’s easy to tell these 3 pie charts look similar, where Trump said the most words and sentences (not surprising). Biden had slightly longer talking time, though he said less sentences. 
```python
n_sen =df.groupby('speaker').agg({"text":'count'}).reset_index()
n_words =df.groupby('speaker').agg({"num_words":'sum'}).reset_index()
speak_time =df.groupby('speaker').agg({"seconds_spoken":'sum'}).reset_index()
def pie_chart(var):
    '''function to make pie chart'''
    labels = 'Wallce', 'Trump', 'Biden'
    sizes = var.iloc[:,1]
    colors = ['bisque', 'tomato', 'royalblue']
    explode = (0.05, 0.05, 0.05)  # explode 1st slice

    # Plot
    plt.pie(sizes, explode=explode, labels=labels, colors=colors,
    autopct='%1.1f%%', shadow=True, startangle=140)
  
    plt.axis('equal')
    plt.show()
    return
```

Pie charts: 1) number of sentences, 2) number of words, 3) speak time

 
  ![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/first_debate/all_pie.png?raw=true){: .center-block :}


Then I focused my analysis on what they said. I did some manipulation to the text data, since while dealing with natural language, we need to perform the pre-processing work like removing punctuation (note: did not to do lemmatization because it would remove "on" from "come on", which is a keyword used later. I may need to revise this part of script in future). After this process, I got a dataframe with 2 columns and 3 rows, with the rows indicating the speakers' text. 
```python
# Lowercase the sentences
df['cleaned']=df['text'].apply(lambda x: x.lower())
# Remove digits and words containing digits
df['cleaned']=df['cleaned'].apply(lambda x: re.sub('\w*\d\w*','', x))
# Remove Punctuations
df['cleaned']=df['cleaned'].apply(lambda x: re.sub('[%s]' % re.escape(string.punctuation), '', x))
# paste words together for each speaker
df1 = df.groupby(['speaker'])['cleaned'].apply(lambda x: ' '.join(x)).reset_index()
df1.columns.values[1] = 'words'
```

In NLP analysis, it never hurt to check the word cloud to get a general idea about who said what. 
```python
# Function for generating word clouds
def generate_wordcloud(df):
    '''generate wold could given speaker'''
    for i in range(3):
        print(df.speaker[i])
        text = df.loc[i,'words']
        wordcloud = WordCloud(max_font_size=50, max_words=100, background_color="white").generate(text)
        plt.figure()
        plt.imshow(wordcloud, interpolation="bilinear")
        plt.axis("off")
        plt.show()
    return

generate_wordcloud(df1)
```

![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/first_debate/cloud.png?raw=true){: .center-block :} 
OK, here’s the main fun part. Based on the drinking game, I create 3 keywords list, 2 for each candidate and one for them both. I assume you needed to have shot when a keyword is mentioned. So I calculated the number of shots based on the game rules as followed.
```python
# create a list of key words for both candidates based on the drinking game rules
trump_key = ['china', 'hunter','fake news', 'great', 'sleepy joe', 'witch hunt', 'space force', 'vaccine']
biden_key = ['malarkey', 'mask', "senate", "vp", 'tax return', 'russia', 'putin', 'come on']
both_key = ['corona', 'covid', 'pelosi', 'obama', 'scotus', 'antifa', 'hilary', 'drug test']
def word_count(key_list,row_n, df1):
    '''function to count frequence of drinking words'''
    total = 0
    for key_word in key_list:
        
        count0 = df1.iloc[row_n,1].count(key_word)
        print(key_word, count0)
        total= total+ count0
    return(total)
```
 ![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/first_debate/shot_t.png?raw=true){: .center-block :}
 ![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/first_debate/shot_b.png?raw=true){: .center-block :}
 ![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/first_debate/shot_both.png?raw=true){: .center-block :}

Too many numbers! So how many shots should you take? For Trump's side, it’s 52 shots. For Biden’s side, it’s 36 shots. Based on Wiki, the smallest standard shot glasses is 1 fl oz(30ml), so that’s 52 fl oz (1560 ml) for Trump's side and 36 fl oz (10800 ml) for Biden’s side. Though I am not a drink expert, I googled and found a popular bottle of Tequila has 12.5 fl oz(375ml). Therefore:
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/first_debate/bottles.png?raw=true){: .center-block :}

OMG! I feel so lucky with my alcohol tolerance. After all I am not willing to pay for so many bottles for a drinking game!

Hopefully you’ve got some idea about how many bottles you need to get for the next game, oh I mean debate. Make the alcohol industry *GREAT* again!

References:

The speakers' pics are from https://our-cartoon-president.fandom.com/wiki/
