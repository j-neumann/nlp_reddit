# Do you need a lawyer, or are you just a jerk?

## Problem Statement

Can you use Natural Language Processing to predict whether a post is asking for legal or personal judgements? In this project, I compare of the two more popular subreddits and attempt to classify a post as belonging to one or the other by training a classification model with content from 9000 reddit posts.

AmItheAsshole is a subreddit for asking strangers to litigate fights between you and your friends/family/significant other in order to determine if you are a jerk. (The answer is usually yes.) It is very popular, with over 650,000 subscribers and posts vary wildly in topic, though they are typically about personal relationships of some sort. But these problems can also be serious- about work discrimination, for example, or about a divorce or marriage that is full of conflict. The personal is often very intertwined with the legal.

LegalAdvice is a subreddit for asking strangers about actual litigation that you may want to pursue, or you are otherwise party to. (It is possible you are also a jerk.) Posts here are often not personal--they are about car ownership, for example, or work problems. But the legal is also personal! People post about problems in their families and in their marriages; posts that are seemingly about legal advice can actually just be about the fact that they were a huge jerk to someone, and are trying to get out of, say, paying child support, or there is a personal conflict that is turning into a very messy legal battle, and backstory is needed for full context.

I expected an initial model to perform well, but get especially confused confused by posts where legal terminology was not used (more common for a subreddit called r/legaladvice than you would guess).

## Executive Summary

I was able to build a model that predicted with 97% accuracy whether a post was from r/AmItheAsshole or r/LegalAdvice. I used count vectorization to tokenize my text into word values, and This model was a logistic regression model with the following parameters: 

Count Vectorizer n-gram range of (1,2)
Count Vectorizer max_features of none
Logistic Regression penalty l1
Logistic Regression alpha 166.81


By adjusting the parameters of my model, I was able to reduce 25% of the error from my initial logistic regression model, taking it from 96% accurate to 97% accurate.

### Contents of Notebook:
- Data cleaning and pulled datasets
- Data Exploration
- Model Preparation
- Model Selection
- Model Analysis

### Data:

I used the PushShift API to scrape 4500 posts from each subreddit. I removed "removed" posts from each dataset, but AITA had about 200 more, meaning that my classes were very slightly unbalanced, at 52% Legal Advice posts to 48% AITA posts. After comparing the results of lemmetized vs unlemmetized models, I lemmetized my data during the data cleaning process.

My predicted class (the variable 1 in my dataset) was Legal Advice. 


### Models Evaluated:

To evaluate this problem, I used logistic regression, a multinomial naive bayes model, and a random forrest regressor. The logistic regression performed the best. I evaluated both Count Vectorizer and term frequency–inverse document frequency as potential word tokenizers, and ended up using Count Vectorizer in my final modelling process.

## Conclusions

It is very much possible to create a model that can predict which reddit one of these posts are in. My accuracy rate of 97% means that, of my predictions, only 64 were inaccurate.

|   |Predicted AITA|Predicted Legal Advice|
|---|---|---|
|**Actual AITA**|917 True Negatives|48 False Positives|
|**Actual Legal Advice**|16 False Negatives|1064 True Positives|

I found it interesting that the rate of false positives was so much higher than the rate of false negatives, which means that the model was more likely to guess that an AITA post was a legal advice post than vice versa. When examining the mistake posts more closely, it became clear that there are definitely phrases involving privacy and work drama that made it hard for the model to understand which subreddit a post came from. Here are some incorrectly classified posts:
![Image_1](https://git.generalassemb.ly/jneumann/Submission/blob/master/Project_3/Images/Screen%20Shot%202019-04-05%20at%208.55.59%20AM.png)
![Image_2](https://git.generalassemb.ly/jneumann/Submission/blob/master/Project_3/Images/Screen%20Shot%202019-04-05%20at%208.58.44%20AM.png)
![image_3](https://git.generalassemb.ly/jneumann/Submission/blob/master/Project_3/Images/Screen%20Shot%202019-04-05%20at%209.02.08%20AM.png)

I found it interesting that many of the incorrectly assumed AITA posts were often written by teenagers or college students--the more casual style of these questions, as well as a lack of legal terminology, confused the model, much like I predicted! It just confused it much, much less than I would have guessed.

I also expected the most impactful variables to contain more legal jargon, but they did not bubble up to the top, for the most part. Here were some of the most impactful variables for each subreddit:

|Legal Advice|
|---|
|doing the|
|males and|
|her husbands|
|timeline day|
|nickname|
|of judgement|
|suspended account|
|zero income|

|Am I the Asshole?|
|---|
|all pitch|
|shield for|
|dad called|
|the fallout|
|withdrawn all|
|cards later|
|our personal|
|repeatedly threatened|


To generate a more perfect model, I would like to collect significantly more data and continue training my model on it. I think that it will better be able to value key legal words as important using more knowledge.




