---
layout: post
title: User research for the PaceTodo app
---

## Table of Contents
* [Introduction](#introduction)
* [Method](#method)
* [Results](#results)
* [Product design](#product-design)
* [Data collection plans](#data-collection-plans)
* [Resources](#references)


## Introduction

Procrastination is one of the most common challenges faced by college students (Steel, 2007). One common cause of procrastination is inaccurate time perception. On the one hand, students who *underestimate* the amount of time needed to complete their assignment might not perceive a need to start working until the last minute. On the other hand, those who *overestimate* the time needed might experience enhanced anxiety and distress that prevent them from focusing on the tasks.

My [collaborator](https://www.charleen.design) and I decided to design an app product to address this issue. In summer 2022, we conducted **foundational user research** by collecting a first wave of data. Below is a summary of the foundational research process. A full data report in pdf can be found [here](/pacetodo.pdf).

The beta version release of the app (Android) can be downloaded [here](https://drive.google.com/file/d/1HYp13UKgArmeWNfYhkw4MGhy26_qfs33/view).


## Method

We collected 52 responses from current graduate students at the University of Pennsylvania. The survey was hosted on [Qualtrics](https://www.qualtrics.com) and contained three types of questions:
1. To what extent do college students experience procrastination?
* e.g. "How often do you experience delay in your plans?"
2. What are the perceived antecedents and consequences of procrastination?
* e.g. "How do you feel when you fail to keep up with your original plans?"
3. When do people find time management apps (un)helpful, and why?
* e.g. "Which time management app (if any) are you using/did you use?"
* "Do you think the app you use is supportive and caring when you fail to keep up with your plans?"


## Results
### 1. Unexpected delays are very common
Around half of the respondents indicate they experience delay half of the time, or more. This ratio is similar between time management app users and non-app users, indicating that **time management apps have limited efficacy**.

![pacetodo-data1](/pacetodo_data1.png "delay frequency")


### 2. Perceived causes of delays

![pacetodo-data1](/pacetodo_data2.png "delay frequency")


### 3. Perceived consequences of delays

Next, we examined respondents' perceived consequences of delays. Over half of the respondents experience either self-blame or anxiety when they fail to meet a deadline. Notably, the proportion of respodents that experience both self-blame and anxiety is considerably higher among app users than non-app users. This suggests that **time management apps generally fail to address the emotional needs of the users**.

![pacetodo-data1](/pacetodo_data3.png "delay frequency")

### 4. Perceived helpfulness of time management apps

Google/Apple calendars and Focus Keeper are the two most commonly used time-management apps. While these apps are generally perceived to be helpful with planning and reflection, they have limited sucess in helping the users execute their planned tasks, and are worse still at providing emotional support to the users.

![pacetodo-data1](/pacetodo_data4.png "delay frequency")

![pacetodo-data1](/pacetodo_data5.png "delay frequency")


## Discussion

Based on the data above, we make the following conclusions:
1. Delays and procrastination are very common among students and can harm not only their academic performance but also their psychological wellbeing. Thus, interventions are needed to reduce delays.
2. Time management apps are popular among students who experience delays. However, most apps focus largely on the planning of tasks and fail to address the behavioral and emotional challenges of delays.


## Product design
To address these limtations, we focus on two key features in our initial design of the PaceTodo app. 
1. First, PaceTodo leverages insight from the **behavioral science of reinforcement learning** by monitoring and comparing users' *anticipated* time with their *actual* time spent and providing feedback accordingly. With adaptive feedback, we hope to help the users develop more accurate time perceptions, thereby alleviating delays.

![pacetodo-app2](/pacetodo_app2.png "time perception training")

2. Second, inspired by findings from social psychology that human beings have an intrinsic need for social connection and support, PaceTodo uses an **anthropomorphized interface to provide companionship and emotional support** to its users. As the app is running, Pacy, an animated cartoon figure will accompany the users and send them reminders when it is time for lunch/dinner/rest. With this design, we hope to provide our users the emotional affordances

![pacetodo-app1](/pacetodo_app1.png "emotional support and companionship")


## Data collection plans

Upon offcial release of the app, we plan to collect app usage data to optimize user experience. Specifially, we plan to collect two types of data:
1. Use machine learning algorithms such as unsupervised learning to detect users' procrastination patterns and provide personalized feedback to improve users' knowledge of their own delay behaviors. 
2. Using an ecological momentary assessment (EMA) approach (Shiffman et al., 2008), we will measure participants' emotional states at various time points during the day, both before after completion of plans, to test the emotional correlates of procrastination. This will enable us to provide personalized emotion regulation training to our users.


-----

## References

Shiffman, S., Stone, A. A., & Hufford, M. R. (2008). Ecological momentary assessment. *Annu. Rev. Clin. Psychol., 4*, 1-32.

Steel, P. (2007). The nature of procrastination: A meta-analytic and theoretical review of quintessential self-regulatory failure. *Psychological bulletin 133*(1): 65.