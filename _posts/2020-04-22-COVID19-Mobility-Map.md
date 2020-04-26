---
layout: post
title: COVID-19 Mobility Map
subtitle: An interactive dash app 
tags: [COVID-19]
comments: true
---

## 1. Introduction
The COVID-19 pandemic has changed everyone's life. While self-isolated as most people, I do feel lucky that I am living in a society where many heroes are fighting with the virus in many ways. Though I cannot be as helpful as our heroes like the doctors and nurses, I did find a way to contribute a little bit--by using my data science skills. Therefore, I plan to work on a series of data science projects regarding to the COVID-19; hopefully I could provide some insights with the perspective of a data scientist.

This is the first project in this **COVID-19** series. I collaborate with [Wentao Duan](https://github.com/wduan31) to create [an interactive dash app](https://covid-19-mobility-map.herokuapp.com/) using Python. This app aims to provide visualizations of COVID-19 cases and mobility change during 2020-02-15 to 2020-04-11 in the U.S. The raw data is provided by JHU CSSE and Google.

## 2. App Description
This mobility map is an interactive app which allows users to check how the pandemic change people's mobility in different places such as retail, parks, and residential places. Users could select options from 4 drop-down lists which provides various ways to visualize the data of their choice.
![img1](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/COVID-19/covid-19-map1.png?raw=true){: .center-block :}
### 2.1 Components of the app
The app includes two main components: four drop-down lists, and charts area
#### * About the drop-down lists
(1) Select National/State: 'national' option only applies to the line chart on the left, 'state' option applies to both charts 

(2) Select a Category: 'COVID-19 Cases' shows the number of confirmed cases and death cases. 'mobility' shows mobility results for 6 different type of places including "retail & recreation", "grocery & pharmacy", "parks", "transit stations", "workplaces" and "residential".

(3) Select a Sub-Category: choose from the 6 different type of places to get the result on the map (right chart)

(4) Select a Date: choose from 2020-02-15 to 2020-04-11

#### * About the charts area
Two charts are provided by this app:

(1) A line chart showing COVID-19 cases or percentage mobility change 

(2) An interactive map to visualize the data selected from the drop-down lists
 
### Raw data resources

(1) The raw data of COVID-19 cases is provided by JHU CSSE, which include both confirmed cases and death.

(2) The raw data of percentage changes is from Google who used the same kind of aggregated and anonymized data for popular times of places in Google Maps. Changes for each day are compared to a baseline value for that day of the week, which is the median value for the corresponding day of the week.

## 3. Insights from the data
### Overview
It can be seen that though the number of confirmed cases have different magnitudes for different states, the trends of percentage mobility change can be very similar. Starting mid-March, most states announced "stay-at-home" orders and closed most non-essential places. The social distance is well represented by the drops of mobility in places such as "retail & recreation" and "workplace". Since most people are encouraged to stay home, the percent changes in residential places have dramatically increased for most states. However, people tend to leave the residential places on weekends.  

### Observations for selected states
#### New York
*keywords*: public transit

<p style="text-align: center;"><img src="https://images.unsplash.com/photo-1574883052806-413e0927a4d7?ixlib=rb-1.2.1&amp;ixid=eyJhcHBfaWQiOjEyMDd9&amp;auto=format&amp;fit=crop&amp;w=687&amp;q=80" alt=" Photo by Kevin Chinchilla" width="311" height="322" /><br /> </p>

<!-- 
 <p style="text-align: center;"><img src="https://i.dailymail.co.uk/1s/2020/03/22/15/26266672-8139923-image-m-59_1584890869653.jpg" alt="1" width="329" height="197"/><p> -->

 
New York's statewide stay-at-home order went into effect on Mar. 22nd, but the New Yorkers' lives started to change much earlier than the order. Mobility in transit stations started to drop as early as on Mar. 9th. People started to spend more time at home and less time in parks since Mar. 15th. Among all the places, the mobility in transit stations decreased the most, with a -72% drop on Apr. 9th compared to the baseline.

#### Washington
*keywords*: parks

<p><img style="display: block; margin-left: auto; margin-right: auto;" src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/32/Mount_Rainier_from_above_Myrtle_Falls_in_August.JPG/450px-Mount_Rainier_from_above_Myrtle_Falls_in_August.JPG" alt="Mountain Rainer" width="322" height="242" /></p>

<!-- <p style="text-align: center;"><img src="https://www.washingtonpost.com/wp-apps/imrs.php?src=https://arc-anglerfish-washpost-prod-washpost.s3.amazonaws.com/public/66K4GPTJUII6VMMZHKLZTRKFCI.jpg&amp;name=small" alt="1" width="329" height="237" /></p> -->

As the first state which officially reported an outbreak, it is interesting to see that the mobility in workplaces dropped to -35% of the baseline on Feb. 17th, showing signs of public concerns about the COVID-19. However, people resumed normal schedulesss to workplaces since then, until the mobility largely decreased again around Mar. 9th. 

It is also interesting to see that until Mar. 23rd, people increased visits to the parks. On Mar. 18th, the mobility in park is +93% compared to the baseline. As a hiker who lived in WA for 2 years, I know that there are a number of great trails in WA, especially in the amazing national parks including Olymic, Mountain Rainer (my favorite!), and North Cascades. But I am still surprised to see people visit parks more often during this time. After some research, I found that this may be because the Trump administration was waiving entrance fees at national parks, from the [news](https://www.washingtonpost.com/climate-environment/2020/03/19/national-parks-fees-waived/). Starting Apr.4th, the mobility in parks jump to be higher than the baseline again while the numbers of COVID-19 cases have been still increasing. Washington hikers, please stay healthy and leave no trace!

#### California
*keywords*: Tourism, tech industry

<p><img style="display: block; margin-left: auto; margin-right: auto;" src="https://images.unsplash.com/photo-1501594907352-04cda38ebc29?ixlib=rb-1.2.1&amp;ixid=eyJhcHBfaWQiOjEyMDd9&amp;auto=format&amp;fit=crop&amp;w=500&amp;q=60" alt="" width="344" height="194" /></p>

<!-- <p style="text-align: center;"><img src="https://pbs.twimg.com/media/EThMd2fXsAMyIop?format=jpg&amp;name=small" alt="1" width="329" height="237" /></p> -->


As another state which owns numerous parks and hiking trails, it's a bit surprising to see the mobility in parks dropped below baseline since Mar. 11th. My guess is most of the visitors to CA parks are not local residents. The tourism industry has been destroyed by the pandemic for sure. 

Though the statewide stay-at-home order was issued on Mar. 19th, people had been dramatically decreasing their stay in workplaces since Mar. 10th. This may be because as the home of many tech companies, it's relatively easier for employees in tech industry to work from home.

#### North Carolina
*keywords*: parks
<p><img style="display: block; margin-left: auto; margin-right: auto;" src="https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/COVID-19/cherry_blossom.jpg?raw=true" alt="cherry blossom" width="279" height="330" /></p>
<!-- <p style="text-align: center;"><img src="https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/COVID-19/cherry_blossom.jpg?raw=true&amp;name=small" alt="1" width="329" height="237" /></p> -->

After living NC for almost 2 years, I found myself really like this state for a number of reasons. Although the state-wide "stay at home" order was issued late in March, NC residents had been taking actions since mid-March, represented by the deep drop of mobility of retail, workplaces and transit stations. Similar to WA residents, people still visit the parks a lot during this time, and the mobility changes are around +40% to +60% from Mar. 8th to Mar. 27th. The beautiful Duke garden is famous for the cherry blossom in springtime (pic above), and this year it barely got any visitors.




