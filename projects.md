---
layout: page
title: Data Science Projects
subtitle: 
---

#### An article search tool for New York Times

- This is a [shiny tool](https://github.com/mingjiezhao/nyt_api_tool) created by R to search news on New York Times based on NYT API. 

The goal of this app is to search for articles from New York Times API on a certain date and output a list of article names. By clicking on an article name listed in the search results, a pop-up window is displayed with more information about the article, including the first image in the article, a head paragraph (snippet), and a hyperlink which directs the users to the article on the New York Times' website.

![shiny tool]: (https://github.com/mingjiezhao/nyt_api_tool/blob/master/pic.png)

#### Latent Dirichlet Allocation

- [Implementation of Latent Dirichlet Allocation ](https://github.com/mingjiezhao/Latent-Dirichlet-Allocation) using Python. 

Latent Dirichlet Allocation (LDA) is a very important model in machine learning area, which can automatically extract the hidden topics within a huge amount of documents and further represent the theme of each document as an ensemble of topics.

Two methods are used to implement the LDA algorithm: Expectation-Maximization (EM) and Gibbs Sampling.

The package is available to install: pip install pip install LDA-project-19

#### SQL databse for USDA food description data

- [SQL databse for USDA by Python](https://github.com/mingjiezhao/USDA_database) 

Are you interested in getting to know more about food we have everyday?

[United States Department of Agriculture](https://www.ars.usda.gov/northeast-area/beltsville-md-bhnrc/beltsville-human-nutrition-research-center/nutrient-data-laboratory/docs/usda-national-nutrient-database-for-standard-reference/) provides great resources about nutritions of daily food.

This project is written in Python to create a SQL database for USDA food data:

-The importdata.py establishs a SQL database (food.db) for USDA data (FOOD_DES.txt)

-The food_query.py takes SQL commends to make queries from the database
