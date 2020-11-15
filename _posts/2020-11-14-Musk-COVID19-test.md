﻿---
layout: post
title: Should Elon Musk worry about his COVID-19 test results?
subtitle: An Introduction to Basic Bayesian Theories 
tags: [COVID-19]
comments: true
---
I believe many people saw the tweet from Elon Musk doubting the COVID-19 tests he took. 
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/COVID-19/Musk_test/tweet.jpg?raw=true){: .center-block :}

It is frustrating when you are not sure if you truly have COVID-19, after taking four times of tests. Similar to Musk, I am also curious to know **what his probability of having COVID-19 is given the 4 test results**. This blog aims to use basic Bayesian statistics to answer this question. Compared to the Frequentist statistics, Bayesian statistics is a theory in the field of statistics based on the Bayesian interpretation of probability where probability expresses a degree of belief in an event [Ref. 1].

I found the following numbers to help me with some calculations later:
* Positive Percent Agreement=0.84, indicating that **84%** people who truly have COVID19 get tested positive with this rapid antigen test [Ref. 2]. 
* Nationally, the overall percentage of respiratory specimens testing positive for SARS-CoV-2, the virus causing COVID-19 is **10.5%** [Ref. 3]. Though it's not perfectly accurate, but we could assume 10.5% of people who took tests are truly positive. 

I am using these 2 numbers for reference here, in the future blog I will demonstrate how the changes of these number affect the calculated results (also known as sensitivity analysis). But now with the test results (2 positive, 2 negative), we can begin our journey of calculating the probability for Musk. 


## 1. What is the accuracy of the test?

When it comes to "accuracy", most people are usually looking for one number. However, in statistics, the accuracy is usually related to two things: **False Positive rate (FP= Pr(test positive\|truly negative))and False Negative rate (FN=Pr(test negative\|truly positive))**. 

I believe most people have heard of these terms but I want to point out the basic Bayesian concept: **conditional probability**. Pr(A\| B) is the probability of event A given event B happens. Maybe you have not noticed but we are actually using conditional probability a lot in daily lives. One simple example would be "the chance you won 1 Million dollars from lottery". This can be seen a conditional probability like Pr(win $1 Mil.\|pay $2 for the lottery). It's pretty fair since you cannot get anything unless you buy the lottery first. Similarly if someone gets a positive result on one test, it does not mean he/she must has COVID19 for true, it means he/she can evaluate the conditional probability of **Pr(truly has COVID19\|test positive)**, based on the FP and FN values.

Ideally we want to small values for both FN and FP. In reality there's always a trade-off between them. When talking about the accuracy of the test, this single number usually means PPA: Positive Percent Agreement=True Positive/(True positive+False Negative). From the FDA document of the test that Musk took [Ref. 2], the PPA is 84%. We will use this number for some calculations later to help Musk!

## 2. Calculation for one single test
Let's start from something simple with only one test result. Before doing that, we can see from the FDA document[Ref. 2], *Negative Percent Agreement* (NPA=True Negative/(True Negative+False Positive) is 100%. In other words, the document is saying FP=0 for this test. So if you tested positive, then you MUST truly have COVID19. However, this conclusion is based on 226 samples, which I think is a quite small number for a pretty reliable statistics. Also I found some news back in September about the manufacture's tests gave False Positives in nursing homes [Ref. 4]. However, I personally don't hold any opinions about the manufacture, and the purpose here is to use some numbers for my calculation. 

Suppose for now we agree with that FP=0 here, so Pr(truly positive | test positive)=1, how do we calculate Pr(truly positive\|test negative)? 
To do that we need to use the Bayes' theorem:
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/COVID-19/Musk_test/theory.jpg?raw=true){: .center-block :}


Here **Event A: truly positive(has COVID19), Event B: test negative**

* Pr(B\|A)=Pr(test negative\|truly positive)= FN =1-PPA =1-0.84 =0.16 

* Pr(A) is the probability of having COVID19. I am using 10.5% as a national number from CDC for week 45 [Ref. 3]. This is calculated as "the overall percentage of respiratory specimens testing positive for SARS-CoV-2, the virus causing COVID-19".
* Pr(B) is the probability of having a negative test result, it equals to: 
    Pr(test negative\|truly negative) * Pr(truly negative) + Pr(test negative\|truly positive) * Pr(truly positive)
    
    =Pr(B\|truly negative) * Pr(1-A) + Pr(B\|A) * Pr(A) 
    
    = (1-FP) *(1-0.105) + 0.16 *0.105
    
    = 0.9118
    
Put them together and use Bayes' theorem:

Pr(B\|A)= 0.16*0.105/0.9118 = 0.018

This means you will unlikely to have COVID19 if you have a negative test result, but it's not impossible.

## 3. How to interpret Musk's 4 test results? Is his chance 50/50?

While it's nice to have FP=0, let's assume nothing is perfect and we have a small FP of 1%. So now it's possible to have a false negative result.

Back to the Musk's test results, we are interested in Pr(truly positive\|4 test results). Here **event A** is still the probability of having COVID19 (truly positive), but **event B** is not a single event anymore, because he did 4 tests (nice to be rich!). To make it simpler, let's first start with the calculations with 2 test results: B1=positive, B2=negative. Then we will move on to the 4 tests situations later. 

Here we need to assume the 4 tests are independent events, meaning one test result has nothing to do with another. It's an important assumption because now we can represent the joint probability Pr(B\|A)= Pr(B1,B2\|A) with the marginal probabilities Pr(B1\|A)*Pr(B2\|A). So we have:

* Pr(B\|A)= Pr(B1=positive, B2=negative\|A)

    =Pr(B1=positive\|A) * Pr(B2=negative\|A)
* Pr(B)= Pr(B1=positive, B2=negative)
    
    =Pr(B1=positive) * Pr(B2=negative)
    
Let's do the calculation with **3 steps**
#### 1) calculate the numerator of Bayesian theorem: 

Pr(B\|A)Pr(A) = Pr(B1=positive\|A) * Pr(B2=negative\|A) * Pr(A)

=Pr(test positive\|truly positive) * Pr(test negative\|truly positive) * Pr(A)

=[1-Pr(test negative\|truly positive)] * Pr(test negative\|truly positive) * Pr(A)

=[1-0.16]* 0.16 * 0.105

=0.0141

#### 2) calculate the denominator of Bayesian theorem:
Pr(B)= Pr(B1=negative, B2=positive)
     =Pr(B1=negative) * Pr(B2=positive)

**a)** In the calculation above, the single text situation Pr(B1=negative) = (1-FP) *(1-0.105) + 0.16 *0.105 = 0.9118, but notice that here we assume FP=0.01. So  
Pr(B1=negative) = (1-0.01) *(1-0.105) + 0.16 *0.105 = 0.90285

**b)** Pr(B2=positive)

   =Pr(test positive\|truly negative) * Pr(truly negative) + Pr(test positive\|truly positive) * Pr(truly positive)
    
   =FP *(1-0.105) + (1-FN) *0.105 
    
   =0.01 *(1-0.105) + (1-0.16) *0.105 
    
   =0.0971

So, Pr(B)=0.90285*0.0971 = 0.0877

#### 3) put numerator and denominator for the final results:
Pr(B\|A)= 0.0141/0.0877 = 0.161

We can see that although some got one negative result and one positive result, his/her probability of having COVID19 is not 0.5!

**Now, the final calculation is for Musk's 4 tests.** Similar to the 2 tests calculation, we just need to multiply things together with the independent assumption to calculate Pr(truly positive\|4 test results). The only difference is that we need to multiply 6 when using the marginal probabilities to represent the joint probability. Here 6 is the value of combination for "4 choose 2".   
* Pr(B\|A)= Pr(B1=positive, B2=negative, B3=positive, B4=negative\|A)

    =6 * Pr(B1=positive\|A) * Pr(B2=negative\|A) * Pr(B3=positive\|A) * Pr(B4=negative\|A)
* Pr(B)= Pr(B1=positive, B2=negative, B3=positive, B3=negative)
    
    =6 * Pr(B1=positive) * Pr(B2=negative) * Pr(B3=positive) * Pr(B4=negative)

#### 1) calculate the numerator: 

 Pr(B\|A)Pr(A)  

=6 * [Pr(test positive\|truly positive)]^2 * [Pr(test negative\|truly positive)]^2 * Pr(A)

=6 * [1-Pr(test negative\|truly positive)]^2 * [Pr(test negative\|truly positive)]^2 * Pr(A)

=6 \* (1-0.16)^2* 0.16^2 * 0.105

=0.0114

#### 2) calculate the denominator:
Pr(B)= Pr(B1=positive, B2=negative, B3=positive, B3=negative)
     =6 \* Pr(B1=positive) * Pr(B2=negative) * Pr(B3=positive) * Pr(B4=negative)
     =6 \* (0.90285*0.0971)^2
     = 0.04614
 
#### 3) put numerator and denominator for the final results:
Pr(B|A)= 0.0114/0.04614 = 0.247

## 4. Conclusions

Glad that you survived with all the calculations! What have you found so far? You may noticed that when you have **2 test results** (half negative half positive), the probability of truly have COVID19 is **0.161**. However, if you got **4 test results** (still half negative half positive), the probability of truly have COVID19 is **0.247**. Why the probability has increased with number of the tests?

The intuition behind the Bayesian statistics is that before we do any test, we would assign our prior knowledge to the calculation (called **prior probability**). Here it is the number of 0.105, the probability of having COVID19. When we performed the test, we would update the probability based on the test result, and this probability is called **posterior probability**. The value of posterior probability is between the prior probability and the observed results (here it's 0.5 because we got half negative half positive). When you do more tests, even though the test results keep the same half&half, you are pushing your posterior probability towards the 0.5 and far from the prior (0.105). That's why you see an increased chance of having COVID19 (0.247 vs. 0.161).

**Two lessons learned from this analysis:**
* The general "accuracy" of the test depends on the prevalence, since it sets the prior probability in the calculation. 
* If you test positive for some uncommon disease (small prevalence in population), it's likely that your doctor to ask you for a second test to confirm. It's possible that Pr(have disease\|one test positive)=0.6 but Pr(have disease\|one test positive)>0.9. I kind of show the idea in the calculation above.

I hope this blog can help you understand better in terms of evaluating the test results. Enjoy using Bayesian and stay healthy!

**References**
1. Wiki page: https://en.wikipedia.org/wiki/Bayesian_statistics
2. FDA document of BD Rapid Detection https://www.fda.gov/media/139755/download
3. CDC report:https://www.cdc.gov/coronavirus/2019-ncov/covid-data/covidview/index.html
4. NY Times: https://www.nytimes.com/2020/10/07/health/nevada-covid-testing-nursing-homes.html