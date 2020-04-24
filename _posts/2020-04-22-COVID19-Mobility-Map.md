---
layout: post
title: COVID-19 Mobility Map
subtitle: An interactive dash app 
tags: [COVID-19]
comments: true
---

## 1. Introduction
The COVID-19 pandemic has changed everyone's life. I am especially very upset that my graduation commencement is postponed. While self-isolated as most people, I do feel lucky that I am living in a society that many heroes are fighting with the virus in many ways. Though I cannot be as helpful as our heroes like the doctors and nurses, I did find a way to contribute a little bit--by using my data science skills. Therefore, I plan to work on a series of data science projects regarding to the COVID-19, hopefully I could provide some insights with a perspective of a data scientist.

This is the first project in this **COVID-19** series. I collaborate with ![Wentao Duan](https://github.com/wduan31) to create an interactive dash app using Python. This app aims to provide visualizations of COVID-19 cases and mobility change during 2020-02-15 to 2020-04-11 in the U.S. The raw data is from JHU CSSE and Google.

## 2. App Description
The app includes 2 main charts: (1) a line chart showing COVID-19 cases or percentage mobility change, and (2) an interactive map to visualize the data. Users could select options from 4 drop-down lists which provides various ways to visualize the data.
![img1](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/COVID-19/covid-19-map1.png?raw=true){: .center-block :}

The raw data of COVID-19 cases is provided by JHU CSSE, which include both confirmed cases and death.
The raw data of percentage changes is from Google who used the same kind of aggregated and anonymized data for popular times of places in Google Maps. Changes for each day are compared to a baseline value for that day of the week, which is the median value for the corresponding day of the week.

## 3. insights from the data
It can be seen that though the number of confirmed cases have different magnitudes for different states, the trends of percentage mobility change are very similar. Starting mid-March, most states announced "stay-at-home" orders and closed most non-essential places. The social distance is well represented by the drops of mobility in places such as "retail & recreation" and "workplace". Since most people are encouraged to stay home, the percentage changes in residential places have dramatically increased for most states. However, people tend to leave the residential places on weekends.  
