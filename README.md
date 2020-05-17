# Project 3: Suicidal Thread Detection Model in Reddit

### Problem Statement
Despite international effort to curb suicide activities, one person still dies every 40 seconds from commmiting suicide. With the rise of internet proliferation, people are moving online to look for advice or emotional support. However, sometimes it might be tagged wrongly - or deliberately - and fall into the other subreddit. Hence, we aim to create a machine learning model that is able to capture any suicidal thread that ended up in the wrong place and transferring them to the care of suicide watcher.

---

### Executive Summary
Suicide rate is often highest in high-income countries, and it is the second leading cause of death among young people [(WHO, 2019)](https://www.who.int/news-room/detail/09-09-2019-suicide-one-person-dies-every-40-seconds). With the proliferation of internet in recent decades, more youngsters than ever have been connected to the world wide web. So it would imperative to utilize the power internet to reach out to these vulnerable young people that has suicidal thought. 

Reddit has been a popular platform for netizens to share their stories or ask for advice. The subreddit of 'Suicide Watch' was created as a platform to empower potential suicide victim, giving them the attention they require and getting them back on the right path.

However, there will be chances that these people have no knowledge of such suicide support-group or simply posted the thread to the wrong subreddit. This would cause the thread to get off the radar of suicide watch and thus the user not received the necessary support from the right community.

So in this project, we set out to create a model to classify thread based on the potential of its content having sign of suicidal thought. We will getting the data from 2 subreddits, one is from the suicide watch of reddit, which will be our positive class (or Class 1). The other subreddit that is used for comparison and as our negative class (Class 0) is the general advice subreddit. Both are similar in nature, with people confessing their problem and sometimes ask for advice from the community. Hence it is expected to show a great contrast.

The data dictionary below described that final data that were cleaned and selected from the data collection via API calls from the official Reddit API:

|Column Name|Data Type|Description|
|---|---|---|
|**full_text**|*object*|The title and content of each thread in Reddit|
|**text**|*object*|Post-processed text of the original full_text|
|**ups**|*integer*|The number of upvotes in each thread|
|**num_comments**|*integer*|The number of comments in each thread|
|**subreddit_subscribers**|*integer*|The number of subscribers in each subreddit|
|**upvote_ratio**|*float*|The percentage of upvotes over the total votes|
|**suicidal**|*binary*|Class of threads, the target variable. 1 represents thread from subreddit suicide-watch, 0 is otherwise|

For the case of our modelling attempt, we will only be considering the 'text' column as the only feature to be fed into the blackbox. This is because if our model were to predict a new post, the thread would not have any of the numerical feature at the beginning of the posting, eg. it will have 0 ups and 0 comments. So our model should be able to perform the classification when they are only bare text made up of the title and its text content.

Two classification techniques, **Logistic Regression** and **Naive-Bayes Multinomial** Model were performed on the dataset to compare their performance on the test data. Each of the technique will be coupled with 2 different types of natural language vectorizer, **Count Vectorizer** and **TFIDF Vectorizer**. The best model was then selected for further analysis and inference.

---

### Conclusion/Recommendation
Our model has successfully classify most of the cases to the correct subreddit, in fact, up to 90% of the thread. However, we have discussed on the importance of reducing the number of False Negative (Type-II error), but the reduction has to be done at the cost increasing False Positive (Type-I error). The optimal point to adjust the threshold can be observed from the AUC-ROC curve of or model.

By tweaking the threshold from 0.5 down to 0.3, our model has became more sensitive in capturing the Class 1 threads. Nevertheless, our model can be further improved by introducing a vote classifier and incorporate some CART (Classfication and Regression Tree) techniques into the pool of model. With this, the different type of model will be to compensate each others' weakness and provide a more accurate classification.

Apart from that, we may also try to include other some subreddit that are similar in nature but not suicidal to increase our sample size. One such example would be r/Confession subreddit. By increasing the sample size, our model will be equipped with a larger word base to better predict the class 0, and in turns improve the overall accuracy.