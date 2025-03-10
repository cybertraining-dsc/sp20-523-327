---
date: 2021-03-15
title: Trending Youtube Videos Analysis
linkTitle: Videos Analysis
tags: ["project", "ai", "lifestyle"]
description: "The internet has created a revolution for how people connect, understand topics, and consume information. Today, the consumption of the media is easier than ever. Going onto the internet and finding interesting content takes less than a minute to do. In the already growing industry of amateur or professional video production, Youtube is one of many go-to platforms for viewers and creators to collide. Social media creates an avenue for Youtubers to help promote their videos and reach a wider audience. For hours on end, viewers can watch nearly any type of content uploaded onto the site. However, it is harder for video creators to make an interesting video any person can enjoy than a viewer to find one of those videos. In the congested mass of videos, how can a Youtuber create a unique identity allowing their videos to go viral? This report will address this issue by creating a prediction of how Youtube popularizes a video and a solution to help a video go viral."
author: Adam Chai
github_url: https://github.com/cybertraining-dsc/fa20-523-327/edit/main/project/project.md
resources:
- src: "**.{png,jpg}"
  title: "Image #:counter"
---

[![Check Report](https://github.com/cybertraining-dsc/fa20-523-327/workflows/Check%20Report/badge.svg)](https://github.com/cybertraining-dsc/fa20-523-327/actions)
[![Status](https://github.com/cybertraining-dsc/fa20-523-327/workflows/Status/badge.svg)](https://github.com/cybertraining-dsc/fa20-523-327/actions)
Status: final, Type: Project

Adam Chai, fa20-523-327
[Edit](https://github.com/cybertraining-dsc/fa20-523-327/blob/main/project/project.md)


{{% pageinfo %}}

## Abstract

The internet has created a revolution for how people connect, understand topics, and consume information. Today, the consumption of the media is easier than ever. Going onto the internet and finding interesting content takes less than a minute to do. In the already growing industry of amateur or professional video production, Youtube is one of many go-to platforms for viewers and creators to collide. Social media creates an avenue for Youtubers to help promote their videos and reach a wider audience. For hours on end, viewers can watch nearly any type of content uploaded onto the site. However, it is harder for video creators to make an interesting video any person can enjoy than a viewer to find one of those videos. In the congested mass of videos, how can a Youtuber create a unique identity allowing their videos to go viral? This report will address this issue by creating a prediction of how Youtube popularizes a video and a solution to help a video go viral.

Contents

{{< table_of_contents >}}

{{% /pageinfo %}}

**Keywords:** youtube, videos, trending, popular, big data, viral, content creation, entertainment, lifestyle


## 1. Introduction

Youtube has two billion monthly active users making it the second-largest social network behind Facebook [^10]. This statistic only accounts for users that login into their Google account while they watch a Youtube video. Hinting, there can be hundreds of millions of more people watching Youtube. Youtube's primary feature during release was to allow anyone to upload videos so the world can watch it. This function has changed drastically throughout the years and turned Youtube into the epicenter for anything to upload a video. Businesses, schools, and even governments are fully invested in Youtube to help promote their content for their respective benefits. Today, being a Youtuber is a respected profession allowing anyone the opportunity to showcase their talent in content production. Youtube is changing the world by exposing their users to the content they would have never experience in person.

This report will investigate trending Youtube videos. Specifically, the report will be using a trending Youtube videos dataset (US only) and will be used to predict how a video will trend on Youtube. Trending videos on Youtube are aimed to surface videos to a wide range of audience who will find interesting. Some content inherently cannot be added to the trending section such as videos primarily containing guns, drugs, etc. There are a lot of hypothesis people created to understand the Youtube algorithm, and the Google Staff has hinted what will make a video trend,

* Are appealing to a wide range of viewers

* Are not misleading, cickbaity, or sensational

* Capture the breadth of what's happening on YouTube and in the world

* Showcase a diversity of creators 

* Ideally, are surprising or novel

but these criteria Youtube has set are not well defined[^1]. Meaning, the determinants, and weights for how a Youtube video will trend will not be explicitly stated and it is up for Youtubers to interpret what exactly will allow their video to trend. In fact, Youtubers have argued the loose standard Youtube created is not true at all. Youtubers are constantly attempting to crack this code, evolving and purposely tailoring their videos in hopes it will go viral. Creating Youtube videos appealing to a wide audience is difficult. It takes enormous creativity and dedication for a random person to enjoy a video found online. Most people on Youtube have specific interests and follow certain industries, however; anyone can appreciate an entertaining video.

## 2. Background Research and Previous Work

After reviewing other background literature and works from other authors within this field, many people have ventured into how a video will be popular on Youtube. Most findings online consist of analysis or unique findings for popular videos. Several people have researched to predict if a video will be popular (views) on Youtube but do not cover the scope if it will reach the trending section on Youtube. Other analysis includes likes/dislikes predictor, comment creator, title scorer, and many more. Additionally, there has been analysis done on topics that are similar to Youtube which can be applied in this instance. A combination of these findings can be helpful and lead this research in the right direction.

## 3. Choice of Data-set

To understand what determines if a video will trend on Youtube the dataset chosen for this project is a trending Youtube videos dataset (US)[^2]. Meaning all videos within the dataset are uploaded from the US and reached the trending section on Youtube. The dataset was retrieved from the popular data science website, Kaggle. The dataset chosen is one of the most popular datasets available on Kaggle and many people have analyzed it. The dataset is known for being readable and having a high usability score.

The Trending Youtube dataset contains 40,949 entries and 16 labels covering the basic information of a trending Youtube video.

| Label      | Description |
| ----------- | ----------- |
| video_id| unique video id|
| trending_date| the date when a video trended on Youtube|
| title| title of the video|
| channel_title| name of the channel that created the video|
| category_id| category of video|
| publish_time| time and date when the video was uploaded|
| tags| keywords associated with the video|
| views| the number of views a video has    |
| likes| the number of likes a video has|
| dislikes| the number of dislikes a video has|
| comment_count| the amount of comments commented|
| thumbnail_link| link to thumbnail picture|
| comments_disabled| boolean variable for allowing comments|
| ratings_disabled| boolean variable for allowing ratings (likes, dislikes)|
| video_error_or_removed| boolean variable if a video is still available|
| description| the description of the video|

A combination of these labels will be used in creating a model to discover how a video will trend on Youtube. The drawbacks of using this dataset are various labels are not covered such as the number of subscribers a channel has or the likelihood of someone that sees the video will click on it and older data is being used (all videos were uploaded and trended between 2017 and 2018).

## 4.Data Preprocessing

All work done on this project was completed through Google Colab. Once the dataset is imported from Kaggle onto Google Colab data preprocessing is necessary to translate the raw data into a readable format. Pandas and Datetime are used for data preprocessing.

To begin there are several labels which can be taken out of the model as they do not appear relevant or cannot be run through the model:

* video_id: this label is a unique identifier for each video not necessary to use
* title: could not be translated into a numerical value
* channel_title: could not be translated into a numerical value
* tags: many tags appear to be irrelevant to the actual video therefore this will be taken out
* thumbnail_link: cannot be run through the model
* description: irrelevant for most videos, does not add value descriptions it appears to promote their channel and sponsors

To address duplicates within the dataset after checking all records there are no duplicates within the dataset, except for empty descriptions. After removing descriptions from the dataset duplicates will no longer be an issue.

Several labels need to be converted into an integer so they can be run through the model:

* trending_date

* publish_time

* comments_disabled

* ratings_disabled

* video_error_or_removed

Pandas reads the trending_date and publish_time labels as objects which need to be changed to integer values. To convert date columns the data type first needs to be converted into datetime. After conversion, another datetime function will be used to separate the month, day, and year into their columns.

![Figure 1](https://github.com/cybertraining-dsc/fa20-523-327/raw/main/project/images/figure1.png)

**Figure 1:** Converting into Dates

Next, the comments disabled, ratings disbaled, and video error or removed can be easily converted with an easy function from their boolean values into 1 or 0 values.

![Figure 2](https://github.com/cybertraining-dsc/fa20-523-327/raw/main/project/images/figure2.png)

**Figure 2:** Converting boolean variables into 1 or 0

## 5. Model Creation and Methodology

There are various ways this model can be built but this project follows the documentation on Scikit-learn. After researching successful methods the model built for this project will be using Scikit-learn Decision Tree and Random Forest. Decision Tree can be used as a multiple regression with a tree-like structure since there is an unlimited number of layers, the decision tree can achieve high accuracy and cause an overfitting problem. Random Forest will randomly select samples and features to train different trees and averages the score of different trees therefore reducing overfitting [^3].

To begin model creation the 80/20, Train/Test Ratio will be used to create the model. In computing, the Pareto Principle is a safe and common approach for model creation[^5]. To determine the accuracy of the model an explained variance score will be applied to determine accuracy. Explained variance is the measure of discrepancy between a model and actual data [^6]. The best possible score is 1.0 meaning there is a stronger strength of association. When creating the model it is important to check if there are highly correlated predictors in the model or else the possibility of multicollinearity can occur. To find highly correlated variables Pearson's correlation coefficient can be used. Correlation coefficients are used to measure how strong a relationship is between two variables [^7]. A value of one indicates a strong positive relationship whereas a negative one indicates a strong negative relationship.

![Figure 3](https://github.com/cybertraining-dsc/fa20-523-327/raw/main/project/images/figure3.png)

**Figure 3:** Pearson's Correlation Graph

When looking at the model it is clear there is a high correlation between likes, dislikes, category_id, and comment_count. Other highly correlated variables to each other include comments_disabled and ratings_disabled, and dates. What this means are videos that disable comments are also likely to disable ratings. The correlation between dates can infer how quickly popular videos will likely trend on Youtube. Assuming the rest of the labels were not necessary or are not optimal the first decision tree and random forest model created consists of the labels likes, dislikes, and comment_count. After scoring the explained variance score the model fell scores around .9.

After going through combinations of labels, when the models had every label it produced the highest explained variance score of around .96. This score is a good result and could mean the models created are very accurate. The reason for a higher explained variance score can be the dates are important if a video will trend. For the visualization, Figure 4 illustrates the relationship between predicted and actual values for views. When examining the image the predicted values are nearly overlapping the actual values. It is very hard to tell any differences. Several discrepancies shown in the image are an over-prediction early within the model and near the end. Although there are over predictions it still closely follows actual values.

![Figure 4](https://github.com/cybertraining-dsc/fa20-523-327/raw/main/project/images/figure4.png)

**Figure 4:** Predicted vs. Actual Values Graph

## 6. Insights

Looking back at Youtube's trending section dividing the dataset into category ids is necessary to discover what content Youtube defines as widely appealing. The figures below show the count of videos in each category and the top 10 categories.

**Figure 5:** Count of videos in each Category     |  **Figure 6:** Top 10 Categories
:-------------------------:|:-------------------------:
![Figure 5](https://github.com/cybertraining-dsc/fa20-523-327/raw/main/project/images/figure5.png)  | ![Figure 6](https://github.com/cybertraining-dsc/fa20-523-327/raw/main/project/images/figure6.png)

Category ID List

| Category ID      | Description |
| ----------- | ----------- |
| 1| Film & Animation  |
| 10| Music   |
| 17| Pets & Animals  |
| 22| People & Blogs  |
| 23| Comedy  |
| 24| Entertainment  |
| 25| News & Politics  |
| 26| Howto & Style  |
| 27| Education  |
| 28| Science & Technology  |

The full list of category IDs can be found [HERE](https://gist.github.com/dgp/1b24bf2961521bd75d6c) [^9]

When diving deeper into the dataset there are clear preferences for videos under certain categories. Entertainment, Music, and Howto & Style categories dominate the trend for categories. This can be an indicator of Youtube's preference for the type of content they want to mainstream on the website.

| **Figure 8:** Entertainment Videos    |  ![Figure 8](https://github.com/cybertraining-dsc/fa20-523-327/raw/main/project/images/figure8.png)|
:------------------------:|:-------------------------:
| **Figure 9:** Music Videos  | ![Figure 9](https://github.com/cybertraining-dsc/fa20-523-327/raw/main/project/images/figure8.png)|
:------------------------:|:-------------------------:
| **Figure 10:** Howto & Style Videos! | ![Figure 10](https://github.com/cybertraining-dsc/fa20-523-327/raw/main/project/images/figure10.png)|

The figures shown are the first three results of a video within their category. Taking a look at the title and comparing them to their category description several videos appear to not fit within their category. The guidelines for the entertainment and howto & style categories do not have set criteria. However, the music category explicitly shows videos based on music most videos under music are music videos from popular artists.

An important task to understand how Youtube picks videos to trend on Youtube is to discover how many channels have trended on Youtube.

| Channel Title | Number of trended videos |
| ----------- | ----------- |
| ESPN| 203  |
| The Tonight Show Starring Jimmy Fallon| 197   |
| Vox| 193 |
| TheEllenShow| 193  |
| Netflix| 193  |
| The Late Show with Stephen Colbert| 187  |
| Jimmy Kimmel Live| 186  |
| Late Night with Seth Meyers| 183  |
| Screen Junkies| 182  |
| NBA| 181  |

Many channels can consistently reach the trending section on a weekly basis. There were 2207 unique channels within the dataset that trended on Youtube. The number of unique channels trending on shows Youtube tries to diversify and promote unique channels on the trending section.

Other insights discovered are the average ratio between likes to dislikes for a trending Youtube video is 20:1. This means for every dislike there are twenty likes. A ratio this skewed is important to consider for a popular video because it is hard to reach this ratio.  Additionally, the average views for a trending video are about 2.3 million views while the average number of comments for a video is 8.4 thousand. A combination of weights of these three statistics can contribute if a video will reach the trending section.

To discover if these insights hold truth comparison of a random video will be selected.

![Figure 11](https://github.com/cybertraining-dsc/fa20-523-327/raw/main/project/images/figure11.png)

**Figure 11:** Randomly Selected Video

The amount of views the video has does not surpass the two million mark but the ratio of likes and dislikes holds at 32:1. The category for the video is music and the amount of comments is far below the average threshold at 1690. Although this video is not reaching certain criteria the ratio of likes to dislikes seems to outweigh the other averages. This signifies a combination of all requirements is important but if any indicator far exceeds the average for the other categories Youtube will allow the video to reach the trending section. 

## 7. Benchmarks

The performance measures for this program were done through Cloudmesh StopWatch and Benchmark[^8]. The instances where the benchmark was measured include loading the dataset, data preparation, timing each model, and the overral code execution. To clarify the performance measures for the program will time how fast sections of code are running through the system.

![Figure 7](https://github.com/cybertraining-dsc/fa20-523-327/raw/main/project/images/figure7.png)

**Figure 7:** Benchmarks

When inspecting the results for the tests, Model 1 took 15 seconds to complete while the final model took 24 seconds. Model 1 contained 4 labels while the final model had 13. By increasing the number of labels there are in the model there is a 62.5% increase in time for execution. The overral code execution took 50 seconds to run which shows the models are RAM intensive meaning it takes a lot of time for the calculations to execute.

## 8. Conclusion

The results indicate engagement from viewers is vital for a video to trend on Youtube. For any video to trend viewers need to like, comment, and even dislike allowing more people to become aware of a video. Videos featuring obscure or illicit content, ie. drugs, guns, nudity, etc., cannot reach the trending section on Youtube because it cannot appeal to a wide range of audiences. Youtube promotes and encourages content any viewer can watch. Several categories such as entertainment, music, and howto & style are some of the most popular categories on Youtube allowing most videos to upload through these categories. Many Youtube channels once they reach the trending section can stay consistent allowing their other videos to have a higher chance of trending. Many Youtube channels adapted to this model producing video content in a similar manner to help reach the trending section. This brings up a flaw within the model of the Youtube trending section. Youtubers are continuously producing content that had success within the past contradicting an important aspect of the trending section stating videos are, "Ideally, are surprising or novel." Various successful channels like ESPN, The Tonight Show, or Netflix are producing videos that are unique but individually are very similar to each other. If a Youtuber is seeking consistent views, producing unique videos until one is successful will help other videos if the content is similar to the successful one. Ultimately, engaging viewer interaction and producing generally accepting content for a Youtuber can increase the likelihood their videos will reach the trending section.

## 8.1 Limitations

Although this current work brings substantial analysis and understanding of this topic the model could be improved in several ways. First, the dataset being used is missing various fields that can impact the likelihood a video will trend such as the number of subscribers a channel has, the number of people that see the video but do not click on the video, and does that channel promote ads on Youtube for viewers to check out the channel. The number of subscribers is available to scrape but the other two fields are sensitive information not accessible to the public. It can be important to have this information because Youtube can prioritize channels uploading content under categories they want to surface or if they pay Youtube to surface their channel. Youtube might be giving private information to help Youtubers become successful. As stated earlier the dataset being used is a couple of years old and the way Youtube promotes videos could have changed within the time frame. Within several years generally accepting content can change. Another limiting factor is the dataset being used only contains videos uploaded within the US meaning it does not account for videos uploaded worldwide. Youtube can prioritize certain content through select regions or this could be meaningless if Youtube promotes the same content throughout the world. The final limitation of this report was not being able to score Youtube video titles and thumbnails. Within Youtube's criteria for popular videos that appear as clickbait will not trend on Youtube. This entails titles and/or thumbnails must have ratings Youtube scores so it does not allow clickbait to surface. Other limitations can include incorrect scrapping and videos that were about to trend. These are various limitations this report faces, however; once this class is over these will be addressed.

## 9. Acknowledgments

Adam Chai would like to thank Dr. Gregor Von Laszewski, Dr. Geoffrey Fox, and the associate instructors in the *FA20-BL-ENGR-E534-11530: Big Data Applications* course (offered in the Fall 2020 semester at Indiana University, Bloomington) for their continued assistance and suggestions with regard to exploring this idea and also for their aid with preparing the various drafts of this article.

## 10. References

[^1]: Google Staff, Trending on Youtube, Google. <https://support.google.com/youtube/answer/7239739?hl=en#:~:text=Trending%20helps%20viewers%20see%20what's,surprising%2C%20like%20a%20viral%20video.> [Accessed Oct 15, 2020]

[^2]: Jolly. Mitchell, Trending YouTube Video Statistics, Kaggle. <https://www.kaggle.com/datasnaek/youtube-new> [Accessed Oct 15, 2020]

[^3]: Li. Yuping, Eng. Kent, Zhang. Liqian, YouTube Videos Prediction: Will this video be popular?, Stanford <http://cs229.stanford.edu/proj2019aut/data/assignment_308832_raw/26647615.pdf> [Accessed Oct 20, 2020]

[^4]: Chai, Adam <https://github.com/cybertraining-dsc/fa20-523-327/blob/main/project/youtubeanalysis.ipynb>

[^5]: Pradeep, Gulipalli, The Pareto Principle for Data Scientist, KDnuggets. <https://www.kdnuggets.com/2019/03/pareto-principle-data-scientists.html> [Accessed Dec 5, 2020]

[^6]: Statistics How Staff, Explained Variance Variation, StatisticsHowTo. <https://www.statisticshowto.com/explained-variance-variation/> [Accessed Dec 5, 2020]

[^7]: Statistics How Staff, Correlation Coefficient Formula, StatsticsHowTo. <https://www.statisticshowto.com/probability-and-statistics/correlation-coefficient-formula/> [Accessed Dec 6, 2020]

[^8]: Gregor von Laszewski, Cloudmesh StopWatch and Benchmark from the Cloudmesh Common Library, <https://github.com/cloudmesh/cloudmesh-common>

[^9]: Prathap, Dinesh. Youtube api video category list, Github. <https://gist.github.com/dgp/1b24bf2961521bd75d6c> [Accessed Dec 7, 2020]

[^10]: Moshin, Maryam. 10 Youtube Statistics, Oberlo <https://www.oberlo.com/blog/youtube-statistics#:~:text=YouTube%20has%202%20billion%20users,users%20than%20YouTube%20is%20Facebook.>[Accessed Dec 7, 2020]
