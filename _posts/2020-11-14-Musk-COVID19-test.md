---
layout: post
title: Should Elon Musk worry about his COVID-19 test results?
subtitle: An Introduction to Basic Bayesian Theories 
tags: [COVID-19]
comments: true
---
I believe many people saw the tweet from Elon Musk doubting the COVID-19 tests he took. 
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/COVID-19/Musk_test/tweet.jpg){: .center-block :}

It is frustrating when you are not sure if you have got the COVID-19, after taking four times of tests. But, how to explain this? Should we not believe any rapid antigen test? I am also curious about the answers so I did some quick analyses based on Bayesian theories and I hope this blog can help you understand better in terms of evaluating the test results.

(Note: compared to the Frequentist statistics, Bayesian statistics is a theory in the field of statistics based on the Bayesian interpretation of probability where probability expresses a degree of belief in an event[Ref. 1])

1. What is the accuracy of the test?
When it comes to "accuracy", most people are usually looking for one number. However, in statistics, the accuracy is usually related to two things: False Positive rate (FP) and False Negative rate (FN). I believe most people have heard of these terms but I want to point out the basic Bayesian concept: conditional probability:Pr(A|B) is the probability of event A when event B happens. Maybe you have not noticed but we are actually using conditional probability a lot in daily lives. One simple example would be "the chance you won 1 Million dollars from lottery". This can be seen a conditional probability like Pr(win $1 Mil. |pay $2 for the lottery). I think it's pretty fair, you cannot get anything unless you buy the lottery first. So if someone get a positive result on one test, it does not mean he/she must has COVID19 for true, it means he/she can evaluate the conditional probability of $Pr(really has COVID19 |test positive)$.This is because there's no perfect, 100% accuracy test, which is understandable.

Obviously we want to small values for both FN and FP. When talking about the accuracy of the test, this single number usually means PPA: Positive Percent Agreement=True Positive/(True positive+False Negative). I found a FDA document of the test that Musk took[Ref. 2], the PPA is 84%. We will use this number for some calculations later to help Musk!

2. Calculation for one single test
Let's start from something simple with only one test result. From the FDA document[Ref. 2], we can see some other numbers, Negative Percent Agreement (NPA=True Negative/(True Negative+False Positive) is 100%. In other words, the document is saying FP=0, and if you tested positive, then you MUST have COVID19(no way you can be negative!). However, this conclusion is based on 226 samples, which I think is a quite small number to get a pretty reliable statistics. There is also news from September about the manufacture's tests gave False Positives in nursing homes [Ref. 3]. I personally don't hold any opinions about the manufacture, and the purpose here is to use some numbers for my calculation. 

So if we agree with that FP=0 here, so Pr(truly positive | test positive)=1, how do we calculate Pr(truly positive | test negative)? 
To do that we need to use the Bayes' theorem:
![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/COVID-19/Musk_test/theory.jpg){: .center-block :}



Based on the table from FDA document:

![](https://github.com/mingjiezhao/mingjiezhao.github.io/blob/master/img/posts_imgs/COVID-19/Musk_test/theorem.jpg){: .center-block :}

Here A: truly positive(has COVID19), B: test negative
* Pr(B|A)=Pr(test negative|truly positive)=5/31=0.16 -> yes it is definition of FN, which equals to 1-PPA
* Pr(A) is the probability of having COVID19. I am using 10.5% as a national number from CDC for week 45 [Ref. 4]. This is calculated as "the overall percentage of respiratory specimens testing positive for SARS-CoV-2, the virus causing COVID-19".
* Pr(B) is the probability of having a negative test result, it equals to: 
    
    Pr(test negative | truly negative) * Pr(truly negative) + Pr(test negative | truly positive) * Pr(truly positive)
    
    =Pr(B | truly negative) * Pr(1-A) + Pr(B | A) * Pr(A) 
    
    = (1-FP) *(1-0.105) + 0.16 *0.105
    
    = 0.9118
    
Put them together and use Bayes' theorem:

Pr(B|A)= 0.16*0.105/0.9118 = 0.018

This means you will unlikely to have COVID19 if you have a negative test result, but it's not impossible.

3. How to interpret Musk's 4 test results? Is his chance 50/50?

While it's nice to have FP=0, let's assume nothing is perfect and we have a small FP of 1%. So now it's possible to have a false negative result.

Back to the Musk's test results, we are interested in Pr(truly positive | 4 test results). Here event A is still the probability of having COVID19 (truly positive), but event B is not a single event anymore, because he did 4 tests (nice to be rich!). Here we need to assume the 4 tests are independent events, meaning one test results have nothing to do with another. It's an important assumption here because now we can have Pr(B|A)= Pr(B1,B2,B3,B4|A), where B1,B2,B3,B4 indicate the 4 test results. To make it simpler, let's first do the calculations with 2 test results: B1=positive, B2=negative. Since B1 and B2 are independent events:

* Pr(B|A)= Pr(B1=positive, B2=negative|A)

    =Pr(B1=positive|A) * Pr(B2=negative|A)
* Pr(B)= Pr(B1=positive, B2=negative)
    
    =Pr(B1=positive) * Pr(B2=negative)
    
Let's do the calculation with 3 steps
1) calculate the numerator: 

Pr(B|A)Pr(A) = Pr(B1=positive |A) * Pr(B2=negative |A) * Pr(A)

=Pr(test positive| truly positive) * Pr(test negative| truly positive) * Pr(A)

=[1-Pr(test negative| truly positive)] * Pr(test negative| truly positive) * Pr(A)

=[1-0.16]* 0.16 * 0.105

=0.0141

2) calculate the denominator:
Pr(B)= Pr(B1=negative, B2=positive)
     =Pr(B1=negative) * Pr(B2=positive)

a) From the calculation, we already calculated the single text situation Pr(B1=negative) = (1-FP) *(1-0.105) + 0.16 *0.105 = 0.9118, but notice that here we assume FP=0.01. So  
Pr(B1=negative) = (1-0.01) *(1-0.105) + 0.16 *0.105 = 0.90285

b) Pr(B2=positive)

   =Pr(test positive | truly negative) * Pr(truly negative) + Pr(test positive | truly positive) * Pr(truly positive)
    
   =FP *(1-0.105) + (1-FN) *0.105 
    
   =0.01 *(1-0.105) + (1-0.16) *0.105 
    
   =0.0971

So, Pr(B)=0.90285*0.0971 = 0.0877

3) put numerator and denominator for the final results:
Pr(B|A)= 0.0141/0.0877 = 0.161

We can see that although some got one negative result and one positive result, his/her probability of having COVID19 is not 0.5!

Now, the final calculation is for Musk's 4 tests. Similar to the 2 tests, we just need to multiply things together with the independent assumption:
Pr(truly positive | 4 test results)
* Pr(B|A)= Pr(B1=positive, B2=negative, B3=positive, B4=negative|A)

    =Pr(B1=positive|A) * Pr(B2=negative|A) * Pr(B3=positive|A) * Pr(B4=negative|A)
* Pr(B)= Pr(B1=positive, B2=negative, B3=positive, B3=negative)
    
    =Pr(B1=positive) * Pr(B2=negative) * Pr(B3=positive) * Pr(B4=negative)

1) calculate the numerator: 

Pr(B|A)Pr(A) = 

=[Pr(test positive|truly positive)]^2 * [Pr(test negative|truly positive)]^2 * Pr(A)

=[1-Pr(test negative|truly positive)]^2 * [Pr(test negative|truly positive)]^2 * Pr(A)

=[1-0.16]^2* 0.16^2 * 0.105

=0.0019

2) calculate the denominator:
Pr(B)= Pr(B1=positive, B2=negative, B3=positive, B3=negative)
    
    =Pr(B1=positive) * Pr(B2=negative) * Pr(B3=positive) * Pr(B4=negative)
    
    = (0.90285*0.0971)^2
    
    = 0.00769
 
3) put numerator and denominator for the final results:
Pr(B|A)= 0.0019/0.00769 = 0.247

4. Conclusions

Glad that you survived with all the calculations! What have you found so far? You may noticed that when you have 2 test results (half negative half positive), the probability of truly have COVID19 is 0.161. However if you got 4 test results (still half negative half positive), the probability of truly have COVID19 is 0.247. Why the probability has increased with number of the tests?

The intuition behind the Bayesian statistics is that before we do any test, we would assign our prior knowledge to the calculation (called prior probability). Here it is the number of 0.105, the probability of having COVID19. When we performed the test, we would update the probability based on the test result, and this probability is called posterior probability. The value of posterior probability is between the prior probability and the observed results (here it's 0.5 because we got half negative half positive). When you do more tests, even though the test results keep the same half&half, you are pushing your posterior probability towards the 0.5 and far from the prior (0.105). That's why you see an increased chance of having COVID19 (0.247 vs. 0.161).

Two simple conclusions from this analysis:
* The general "accuracy" of the test depends on the prevalence, since it sets the prior probability in the calculation. 
* If you test positive for some uncommon disease (small prevalence in population), it's likely that your doctor to ask you for a second test to confirm. It's possible that Pr(have disease | one test positive)=0.6 but Pr(have disease | one test positive)>0.9. I kind of show the idea in the calculation above.

Hope you will enjoy using Bayesian and stay healthy!

References
1. Wiki page: https://en.wikipedia.org/wiki/Bayesian_statistics
2. FDA document of BD Rapid Detection https://www.fda.gov/media/139755/download
3. NY Times: https://www.nytimes.com/2020/10/07/health/nevada-covid-testing-nursing-homes.html
4. CDC report:https://www.cdc.gov/coronavirus/2019-ncov/covid-data/covidview/index.html