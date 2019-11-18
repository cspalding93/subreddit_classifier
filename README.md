# Natural Language Processing and Classification Models
### Discerning posts between the subreddits "DIY" and "Crafts"
__________________
**Author: Charles Spalding**

## Problem Statement
_____________
A majority of information available is unstructured information in the form of natural language. The analysis of natural language provides some of the most valuable insights in data science. Thorough analysis allows insights into documents such as topic analysis and probability of buying a product. By collecting posts from two subreddits, we can see the effectiveness of various methods on discerning which of the groups the posts came from and what topics emerge from the data sets.


## Executive Summary
_________________________

The data was collected from reddit by using their api and their developer page. I decided to look at subreddit topics that are neither terribly separate nor incredibly overlapping. DIY and crafting were perfect for the challenge. I initially collected 7,500 posts from each subreddit. After I removed the posts marked as either 'deleted' or 'removed', the data set contained a little over 12,000 posts.

The title and body of the posts were the primary focus when performing NLP modeling. When the two are put together, every post contained the necessary text for classification modeling. The two NLP vectorizers in the sklearn library are the CountVectorizer, which provides a word count sparse matrix, and the TFiDFVectorizor, which provides a weighted matrix for the word presence in the corpus. I used a Pipeline and Gridsearch to determine the optimal settings of the two vectorizers. TFiDFVectorizor (TFiDF) was decidedly better performing than the CountVectorizer by a small margin when passed through a logistic regression. For further preprocessing, I used stemming and lemmatization to correctly group the words together for analysis. Stemming is the more aggressive method and performed better with TFiFD. 

Multiple models were instantiated and fitted to produce a better score than the baseline. The baseline was at 54% accuracy for guessing all of the posts as the 'crafts' page. The logistic regression models and the Gaussian Naive Bayes performed moderately, scoring 83.1% and 83.6% respectively. Two decision tree methods were used as well; however, both the random forests and the extra trees performed worse than all other models. The best model at the end of the project was the support vector classifier at 85.3% accuracy. 

Topic analysis provided crucial insight to the data as well. I used the Non-negative Matrix Factorization method on the separate subreddits, combined dataset, and the misclassified posts. This allowed insight into the data that would not have been possible by looking at word counts. Threads asking for advice/direction on a project and repairing various objects were distinctly unique to the DIY subreddit, whereas the crafts section had more consistent posts about creating small gifts, jewelry, or making home decor. When combined, two themes emerged: posts linking to easy tutorials videos and posts asking for opinions on the final product from the online community. 

To explore the posts that were more consistently misclassified, I performed two actions:

1. I used my best model, the SVM, to make a prediction column in order to explore the misclassified posts. I found that a little over 20% of those misclassified were posted between both of the subreddits; a phenomenon known as "double posting". A small portion was also posted repeatedly in the subreddit. These are methods that users on Reddit often use to collect "Reddit Gold," or "brownie points" of the website. 

2. I performed topic modeling on the rest of the misclassified to reveal themes in the model's error. Posts that were misclassified as crafts either explicitly mentioned the size of the project--such as making a mini set of furniture for a doll house, or explained how the project was for a friend or holiday. Posts that were misclassified as DIY either used components that are typically reserved for bigger tasks--such as plaster or larger woodcrafting, or sought to repair something electronic or mechanical. 

## Conclusion
______________________

I was able to train a support vector machine classifier to outperform the baseline model of 54% accuracy. **My best model performs with an 85% accuracy along with 3% explainable error**. All models performed within a relatively similar range of accuracy, but the SVM not only broke the 84% threshold I was unsure of reaching, but achieved 85%. 

The topic modeling performed by the NMF allowed insights that were crucial into understanding the misclassification. Given the context of the topics of the overall corpus and the misclassifications, it was understandable that there was such a high error margin on posts. This analysis gives a deeper understanding into the data

Lastly, as reflection of the project, the insights into the misclassifications are just as valuable as optimizing the models themselves. And exploring themes in a corpus is key to explaining your model's performance. I would recommend topic analysis when exploring textual data as it provides insights that can be easily interpreted.