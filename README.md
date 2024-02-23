# SentimentAnalysis
Varios projects on Sentiment Analysis applied to finance

# Abstract
It is clear that news headlines carry enough information to influence the stock market. In this project we will try to discern this impact and its speed by analysing the language used in financial news headlines to try and correctly assess word by word impact by using Natural Language Processing and Machine Learning. Using delta S&P 500 price as our proxy we will then test a recently scrapped news dataset and compare it with reality, finding similarities in trend and a relatively small margin of error in function of the predicted window size and the sensibility of positive and negative tokens.

# Introduction

News frequency seems to be getting faster and faster, and to get their information from ever deeper and inside sources. But are they so fast that they could overpace the stock market with information unknown to investors, creating a gap and an arbitrage opportunity? 

Stock markets are known to not be perfect but more and more theories sustent their semi-strong efficiency, and as such it would seem impossible to see global news being faster than stock prices. If stock prices are deemed predictable with news headers, it would be a huge opportunity for whoever can react instantaneously to a news header or article - which is with machine learning, accessible to anyone - and would certainly lead to the downfall of the stock market.

What stems from Smith and O’Hare paper on Comparing traditional news and social media with stock price movements; which comes first, the news or the price change?; is that apart from very rare occurrences, stocks are already up-to-date with news information.
We tried to forge our own opinion on this subject, by computing a database of news headers, and with the help of sentiment analysis try to determine a trend between stock market and news headers. 

# Brief Literature Review

In A picture is worth a thousand words: Measuring investor sentiment by combining machine learning and photos from news (April 2022), published at the Journal of Financial Economics, authors Obaid and Pukthuanthong fiercely highlight the relevance of news in investors behaviour. Even though the authors focus their attention on images included in news and how they create a “pessimism” effect that affects investors behaviour. They aso pay special attention to how language included in news contributes to the mentioned “pessimism” effect in a complementary or substitutive way to the photo pessimism, mostly during high volatility or fear periods. In addition, their machine learning approach is strong  at image interpretation, which will be correlated with stock returns in order to create an investor sentiment index whose correlation is stronger towards downwards stock return deltas.

On the other hand, as mentioned in Stock trend prediction using sentiment analysis (March 2023), published at PeerJ Computer Science, authors Xiao and Ihnaini differ slightly in the approach by using tweets and news as their natural language processing vehicle to analyse and predict stock returns.The authors, most importantly compare those tweets ad news generated on the entire natural day to those posted only on opening market hours, finding that tweets and news posted only in market hours statistically outperform those posted during any moment in the day. Authors emphasise in the fact that stock price predictions done by the use of natural language processing should mostly be done in the short horizon as market sensitivity to information fluctuates significantly form one stock to another, therefore average effect could be diluted in time.

Finally, as stated in Sentiment and uncertainty (2022), published at the Journal of Financial Economics, authors Birru and Young hold that sentiment analysis exhibits its stronger effects at times where stock estimations are most volatile and thus subjective, implying that when investors do not reach a collective stable price, thus high volatility, informational shocks have their highest impact. Authors reach the conclusion that their sentiment analysis model is up to four times more efficient when uncertainty is higher than its mean, meaning that stock prices are most susceptible to change in direction of what's published and the amount of investors that actually have access to this information. It is also highlighted that the reaction time may vary by multiple factors, mostly in function of the stock, market and source. It is evident that by composting an index market effects are condensed but most importantly general uncertainty is crucial to a high precision.

# Methodology

As financial news have a high daily frequency even when the markets are closed, it is important to understand the time span in which those news make an impact and actually create an influence in the market. That's why financial news providers are a key player in understanding the market itself. For our study, the chosen data provider was FinViz, which is a free financial data visualisation website that collects news in real time from important financial institutions such as Reuters, Forbes, MarketWatch, Wall Street Journal, among others. Thanks to its open API we were able to scrape real time information from their webpage beginning on October 25 2023 up to November 24 2023, providing a dataset of about 1.050 data points.  

Nevertheless, in order to properly train our model, our approach required a much larger dataset of news headers in order to properly establish the weights certain words indeed have in influencing the market, that is in our study S&P 500. We chose S&P 500 as a world-size financial index open to all types of industries, which we thought would be the closest to what stems from global news. As this dataset was used to train the model, any other news dataset will fit perfectly if it is considered more accurate or contains sector-specific news that can be considered more relevant to understand an impact or to discern in between market influence factors. This dataset covers daily news from June 8th, 2008 up to July 1st 2016.

As part of the training process, we matched daily values of the S&P 500 with our dataset of news headers so that relevance of certain words could be obtained by the use of supervised learning. The impact was measured on stock variation which is a proxy for the delta in between the daily close and open price of a certain stock (here S&P 500). 

From this matching process we summed the stock variation happening at each word’s appearance in news headers, and got a list of words associated with a weight (which is the combined sum of stock variation). 

In order to clean the dataset and extract only the relevant and significant words, we computed a list of neutral english words (articles, pronouns,...) which we deleted from this list.

Consecutively, for each day of our Finviz dataset we computed the sum of the associated values of the words in the news headers, i.e. each of the news headlines has an associated total value according to the words that contains. Then for each day of news articles from October 25th to November 24th we got a total value, supposed to represent the stock variation happening during this day, according to the weights of our model. 

The variables on which we could vary to adjust the model weights are:

The window of days used to compute the weight, that is which stock variation you associate to a header. For our analysis, we had three choices, one day (the variations on the day of the news), two days (variation on the day plus the day after) and three days (same with the day before, to account for potential asymmetric information).

The weights of stock variation, that is whether we choose to sum the variations for a word as they are, or if we change their weights. We saw that if left as is, stock variations being in general positive, the weights of each word tends to be positive. Our better estimates were computed when negative stock variation for the period had higher weight than positive ones. Also, it helped rescale the variations to make it closer to reality.

Finally, with the purpose of testing the model we established the predicted values of our dataset and compared them to the real values of the S&P 500 index over the last month, starting on the same point, and as our proxy are variations we could then just calculate the period t+1 as the result of period t plus the established variation.

# Results 

After training our model with historic data by computing word values based on the historic occurrences on the previous stated news dataset and then giving them values due to the S&P 500 price delta, we apply the model into our dataset and try to predict the future price variations starting from a determined point and price. Following the mentioned literature, estimations were done on the 1.050 data points financial news dataset scrapped from FinViz, and price variations were done only on labour days where market was open, restricting ourselves to a short time horizon so the prediction is more accurate.

# First result

Our first result is the stock variation induced by our model, starting at 4240 $ to start at the same point of S&P 500 on the 25th October 2023, and with weights for each word reduced to 0.45 of the original value for the negative stock variations and 0.33 for the positive stock variation - here again, to scale to S&P. The weights in these first results are computed from the stock variations happening on the day the news headers got out.

Sentiment analysis results with weights of 0.45, on one day 
Now by plotting the S&P 500 index in the same specified dates:

S&P 500 on the same period

We can see a certain global trend which is the same in our analysis and in S&P 500, which would confirm the correlation between the Stock Market’s prices and the News Headers. 

# Subconsequents analysis

To strengthen and try to better fit our model, we played on the number of days taken in account, and the weights induced by negative and positive stock variation separately. 

Comparison for 3 days and weight_p 0.25 weight_n 0.40

Comparison for 2 days and weight_p 0.33 weight_n 0.45

We get our better fit with stock variations on two days (ie, the day of the news header and the one after), and custom weights for positive and negative stock variation of 0.33 and 0.45 respectively. 

As it is possible to appreciate sentiment analysis predictions by using natural language processing does manage to reflect S&P 500 behaviour in the short term. Nevertheless, it is clear that our prediction fits depend drastically on the sensitivity chosen, meaning that in order to accurately predict a longer horizon it is necessary to constantly adjust these weights in the way that they continue to fit most of the points or at least the general trend.

# Comments and points of improvements of our model:

The training Dataset of News headers used to compute the weights of our model. It isn’t easy to find a huge dataset of finance related news headers. The one we chose stops in 2015, so maybe we miss some recent words which became relevant in the finance industry afterwards. This also affects the weight affected to each word, but the advantage of this dataset was that it comprised the 2008 financial crash, so we had enough negative stock variation to counter balance the positive ones.

We chose to evaluate and compute our model on the S&P 500 index. We thought it was a big enough/well-known index to show the trend of the global market, nevertheless it is also true that given the composition of this index its hard to find enough news dataset to cover all the underlying industries in the best possible way, and given the vast amount of companies in it it's perfectly possible that a news headline affects its companies both positively and negatively, given a margin of uncertainty. 

Before evaluation with our model, and during the computation of our model, all words are tokenized, thus passed in lower case letters and single tokens. Maybe we can miss/confuse words between themself. We anticipated and prevented  some of the cases, such as the confusion between the US and us. As well, it is possible that starting words of news headlines may create a higher impact than those in the middle or compound sentences may affect the value of certain words.

English stoppers could always be improved. We tried to remove from the dataset all non related common language words such as pronouns, connecting words and such, but we may have missed some in the process, falsifying a bit the evaluation.

This model doesn’t account for the sense of a sentence, and only estimates the global value of it word by word. It also doesn’t take into account the numbers which may be found in a news header (ie, a rise of 1% and 10% shouldn’t have the same value). 

The model doesn’t differentiate between news sources. There are certain news providers with higher impact and reach than others, as the model does not differentiate between them it could create an unseen impact in price variations.

# Conclusion

Our model seems to suggest that, at least on the period tested, News Headers and Global Market Stock Variation reflect each other. This is even fitting surprisingly well, but is still not so shocking since Stock Markets are in the end, the mirror of World Events.

We didn’t answer the question of prediction of the Stock Market, since we can only infer the movement of the Market after the day is finished and all news headers are taken into account. Nevertheless, it is indeed possible to suggest further approaches in order to answer this question, mean prediction in a 3 day period, automatic adjustments given specific lag values or even a pseudo-random prediction coming from the value for a mobile average. 

Ultimately, the aim of this study is to seek and somehow materialise the relationship between news headlines and the market itself for a real and short timestamp, as suggested per our literature review, for this Natural Language Processing proved to be useful and accurate, giving as well significant margin of improvements.


# Bibliography

Khaled Obaid, Kuntara Pukthuanthong,
A picture is worth a thousand words: Measuring investor sentiment by combining machine learning and photos from news,
Journal of Financial Economics,
Volume 144, Issue 1, 2022, Pages 273-297, ISSN 0304-405X, https://doi.org/10.1016/j.jfineco.2021.06.002.
Xiao Q, Ihnaini B. 2023. Stock trend prediction using sentiment analysis. PeerJ Computer Science 9:e1293 https://doi.org/10.7717/peerj-cs.1293
Justin Birru, Trevor Young, Sentiment and uncertainty,
Journal of Financial Economics,
Volume 146, Issue 3, 2022,Pages 1148-1169,ISSN 0304-405X, https://doi.org/10.1016/j.jfineco.2022.05.005.
Stephen Smith, Anthony O'Hare (2022 Apr 28), Comparing traditional news and social media with stock price movements; which comes first, the news or the price change?
