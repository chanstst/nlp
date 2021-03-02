# Natural Language Processing for Social Media Posts

### Problem statement

We are a team of political advisors, and our job is to provide insights to political and business groups on the current political landscape, and how they should steer their policies and strategies.

The goal of this project is to build a classifier on which subreddit a given post came from. By researching the popular texts among Republican and Democrat supporters, we expect to extract key issues facing the population and assess their sentiment, especially on the key words.

Two subreddit groups are used:
- r/Conservative
- r/democrats

### Workflow summary

Two major workflows in this project:
1. Webscrapping: using Reddit's API, I collected around 1000 posts from each of the two subreddits, and the related comments
2. Natural Language Processing: I created two models (Mulitnomial Bayesian and Logistic Regression) to train classifiers.

### Webscrapping via Reddit API
- Reddit API allows a vast amount of data to be downloaded in json format
- Two levels of crawling, first on the page with a list of posts, then the page of individual post and related comments
- To minimise the loading on Reddit server, special care was taken to add some latency in-between html requests
- Data crawled was saved in csv after removing non-characters in text fields, to ensure the information was saved properly in csv format
- Key fields were referred to: 1) name (id), 2) title, 3) comments, 4) selftext

### Data processing
- removing non-characters in texts
- lemmatizing
- removing English stop words
- removing additional stop words manually

### Vectorization
- CounterVectorization

### Modelling
- Logistic Regression
- Multinomial Bayesian
Logistic Regression was able to provide a better accuracy, around 75% in validation sets as well as test sets

### Modelling accuracy
- Achieved 75% accuracy on the test dataset, vs base case accuracy of 50%
- Model performances are similar, after fine-tuning hyper-parameters. Maximum number of features is a key determinant in both CountVectorizer and TF-IDF Vectorizer
- Stemming - no major difference in model accuracy with or without stemming

### Data Visualization
By studying the key words effective at differentiating "Democrats" vs "Republican", some insights were derived:

#### Democrats
- Democrats are more prone to mentioning "donald", "trump", "cruz", "republican", "right wing"
- Due to the recent news, "impeachment", "insurrection", "capitol", "resign" are the key identifiers in Democrats' posts
- Democrats also mention more "democracy" and "inauguration" in the posts, which seem to be what they are concerned

#### Conservatives
- "China", "communist", "leftist" are the top words to identify the posts of Conservatives
- "fraud", "evidence", "ballot" are related to recent news on election
- Conservatives tend to talk more "deal", "business", "tech", "big tech"

### Insights from key words
After refitting the model with the best parameters, the weightings of model coefficients were ranked and the more "influential" key words were examined. Comparing this list with the most common key words in the corpus, it was confirmed that the most popular words in the corpus may not be the most effectively in classification, ie the model was able to extract important key words from each class.

Those key words are good indicators of the current political landscape in US.