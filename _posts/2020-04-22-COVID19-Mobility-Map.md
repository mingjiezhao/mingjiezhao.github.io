---
layout: post
title: COVID-19 Mobility Map
subtitle: An interactive dash app 
tags: [COVID-19]
comments: true
---

## 1. Introduction
The COVID-19 pandemic has changed everyone's life. While self-isolated as most people, I do feel lucky that I am living in a society that many heroes are fighting with the virus in many ways. Though I cannot be as helpful as our heroes like the doctors and nurses, I did find a way to contribute a little bit--by using my data science skills. Therefore, I plan to work on a series of data science projects regarding to the COVID-19, hopefully I could provide some insights with a perspective of a data scientist.

This is the first project in this **COVID-19** series. I collaborate with [Wentao Duan](https://github.com/wduan31) to create [an interactive dash app](https://covid-19-mobility-map.herokuapp.com/) using Python. This app aims to provide visualizations of COVID-19 cases and mobility change during 2020-02-15 to 2020-04-11 in the U.S. The raw data is provided by JHU CSSE and Google.

## 2. App Description
This mobility map is an interactive app which allows users to check how the pandemic change people's mobility in different places such as retail, parks, and residential places. Users could select options from 4 drop-down lists which provides various ways to visualize the data of their choice.
![img1](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/COVID-19/covid-19-map1.png?raw=true){: .center-block :}
### Conponents of the app
The app includes two main conponents: four drop-down lists, and charts area
#### About the drop-down lists
(1) Select National/State: 'national' option only applies to the line chart on the left, 'state' option applies to both charts 
(2) Select a Category: 'COVID-19 Cases' shows the number of confirmed cases and death cases. 'mobility' shows mobility results for 6 different type of places including "retail & recreation", "grocery & pharmacy", "parks", "transit stations", "workplaces" and "residential".
(3) Select a Sub-Category: choose from the 6 different type of places to get the result on the map (right chart)
(4) Select a Date: choose from 2020-02-15 to 2020-04-11

#### About the charts area
Two charts are provided by this app:
(1) A line chart showing COVID-19 cases or percentage mobility change 
(2) An interactive map to visualize the data selected from the drop-down lists
 
### About the raw data
The raw data of COVID-19 cases is provided by JHU CSSE, which include both confirmed cases and death.
The raw data of percentage changes is from Google who used the same kind of aggregated and anonymized data for popular times of places in Google Maps. Changes for each day are compared to a baseline value for that day of the week, which is the median value for the corresponding day of the week.

## 3. Insights from the data
It can be seen that though the number of confirmed cases have different magnitudes for different states, the trends of percentage mobility change are very similar. Starting mid-March, most states announced "stay-at-home" orders and closed most non-essential places. The social distance is well represented by the drops of mobility in places such as "retail & recreation" and "workplace". Since most people are encouraged to stay home, the percentage changes in residential places have dramatically increased for most states. However, people tend to leave the residential places on weekends.  
