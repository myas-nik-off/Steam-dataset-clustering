# Steam-dataset-clustering

Data Clustering of Steam Dataset.


## Introduction

Steam - one of the biggest gaming platforms in nowadays world with a lot of functions and games, you can find pretty much everything from the gaming industry there. Mainly, Steam is a huge shop for distribution of digital game copies. It was created by a game company called Valve in 2003 and since then has developed into a social network around games. (Valve Corporation, 2022) Being a gamer myself and having love top this industry since my childhood, I decided to make a project on the data from Steam. I was curious about interesting findings which I could have found making this data analysis. Indeed, the information presented here might be interesting not only to other fellow gamer comrades of mine but also to the wide variety of people from different backgrounds - that is what I hope for. Have you ever wondered how much money a developer can make from a game? Or what happens with the digital game copies which you bought after your death? There a lot of issues and questions that we have in the game industry, and all of them are quite intriguing. There is this worldwide tendency for older generations to neglect and underrate the importance of video game and other digital content. Yet, in this paper I would concentrate only on the factual data from Steam platform and make some sense to it by doing analysis.


## Dataset

The dataset was taken from the Kaggle website and was published by Vicente Arce in February 2022. The dataset consists of raw game data extractions from the Steam Store API and the Steam Spy API. There are two files originally "steam_app_data.csv" and "steamspy_data.csv" weighing 124 MB together. (and 688.89 MB after a mathematical sum of their properties) "steam_app_data.csv" data file contains 39 features and 66,414 unique values; whereas, "steamspy_data.csv" data file has 20 features and 63,504 unique values. The features contain information like the type of application, application name, unique application Steam id, age restriction, free-to-play characteristics, DLC (downloadable content) availability, descriptions of application, supported languages, PC (personal computer) requirements, developer's and publisher's names, availability of Demo (demonstration of a product), platforms, reviews from critics and users, categories and genres, release date, count of the user owning an application, current and initial prices, discount (if there is any at the moment of the original data collection), amount of CCU (Concurrent Users) in an application, and other. That much data is a great treasure for the data analyst, as you can make so many different calculations and have a lot of valuable results.

Source: Vicente Arce. (2022). Steam and Steam Spy raw datasets. Available from: https://www.kaggle.com/datasets/vicentearce/steam-and-steam-spy-raw-datasets?select=steamspy_data.csv. (Accessed 18 November 2022)

Coding Environment: ANACONDA.NAVIGATOR's jupyter Notebook (6.4.8) for macOS
Language: Python 3.6


## Aim

The main purpose of this analysis is to apply Big Data analysis techniques like clustering to real data. The specific aim with this dataset is to explore the relationships between genres/categories of applications and various parameters such as price, initial price, discount, median and average minutes of gameplay since 2009 and in two weeks of February 2022, ratings, digital copies owned by users, and CCU. This will help understand which game genres are currently popular and which categories are trending in the game world market. As a secondary goal, I have looked for any interesting findings during the analysis.

Sub-goals include comparisons of:

• The most popular application tags
• Amount of applications released on the platform in 20 years
• The dominating game industry developers and publishers
• The proportion of free and paid games
• Types of applications in the dataset in general
• The proportion of games with DLC
• Amount of application Demos on the platform
• Age restrictions among games
• The most demanded platforms for games
• The most used languages


## Analysis

For the initial analysis, I combined "steamspy_data.csv" and "steam_app_data.csv" into one dataset named "data" by comparing both to the "steam_appid" feature, and I cleaned up repeated columns and values. The new dataset had 52 features (columns) and 66 902 applications, mostly games (raws).

• Tags: Tags are user-given characteristics to a game, and the analysis showed the most popular game tags. The most common tags are 'games without any tag', Indie & Casual, and Action & Indie; 15,522 applications have no tags, and Indie & Casual is the second most common with 296 uses. There are 428 overall tags.

• Release Date: Games on Steam date back to 1895, according to the data, but this is likely a developer joke, as future dates like 3021 also appear. 6,991 games have no date, and 2021 saw the peak release of 12,371 Apps. The trend indicates increasing application development each year due to technological advancements.

• Developers: The major developers, according to the dataset, are "Choice of Games" with 144 titles, "Laush Dmitriy Sergeevich" with 113 games, and "Creobit" with 102 applications. Despite the high number of games, this doesn't equate to quality, as these aren't well-known AAA+ game developers.

• Publishers: Game publishers are key to the industry's financial aspect, with "Big Fish Games" owning 416 games on Steam, followed by 377 'non-developer' games and "SEGA" with 168 games, a more recognizable name. 

• Free Games: Free-to-play games are gaining popularity, with companies like "Epic Games" offering free games weekly as a marketing strategy. On Steam, 7,533 out of 59,122 games are free.

• Type: Aside from games, there's only one advertising and one hardware application.

• DLC: About 0.14% or 9,342 games on Steam have DLC, and 6,009 are demo versions, just 0.09% of the entire library.

• Required Age: 98.07% of applications don't specify age restrictions, indicating a need for more regulatory development in gaming. 

• Platforms: Windows is the most supported platform with 49,872 Apps, and 7,910 Apps are cross-platform.

• Languages: English is the most common language in 19,098 games, followed by English and Russian in 1,598 games.


## Unsupervised Analysis

Unsupervised method is needed for much more complicated analysis regarding this data. Unsupervised Analysis can show a huge difference between a normal data analysis and a learning algorithm. In order to find correlations between different features and the numbers themselves, I have used K-Means Clustering. For the main purpose of the analysis, I took the data corresponding to: Steam Application ID, Genres, Categories, Prices, Initial Prices, Discounts, Game Owners, Median Playtime since March 2009 (in Minutes), Average Playtime since March 2009 (in Minutes), Median Playtime in the Last Two Weeks in February 2022 (in Minutes), Average Playtime in the Last Two Weeks in February 2022 (in Minutes), CCU, Positive Ratings, Negative Ratings, and User Score.

After cleaning the dataset by: extracting numeric values from Genres, Categories, Amount of Sold / Distributed Copies, Discounts in Percentage, converting currency of Price List and Initial Price from Euro (EUR) to Pound Sterling (GBP) (1 EUR = 0.88 GBP on 14.11.2022) (BBC, 2022), and removing NaN, (Not-A-Number, but usually the evidence of empty space). I decided to drop 0 values from: 'genres', 'owners', 'median_forever', 'average_forever', 'positive', 'negative', and 'userscore' columns trying to make the clustering result better and ended up with the table of 128 rows. Then, the scaling data normalisation was done as the values' range differed a lot. It is needed for the algorithm to find a better result for the clustering. 

After scaling, K-Means Clustering was done with a repeating loop of 23 times. The result for Silhouette Coefficient has been becoming better with every new iteration of the code. The mean Silhouette Coefficient of all samples shows overlapping of just created clusters - the more value closer to 1, the less overlapping there is. The completeness Metric of Cluster Labelling is the second value in the table. It shows to which extent the values of one class are clustered together or not. The highest score that we can observe here is 0.41, which is far from the ideal 1 but at least not 0 or negative. The Homogeneity Metric of a Cluster Labelling is the last value out of three, and it shows if clusters contain the data points from the same class only. The highest rate in the example on the left is 0.4 - it's not much and far from the desired outcome of 1. 

As a result, we can see some kind of causation-relationship, not a correlation, between the values. To have a more desirable outcome, there should be done more tests and, probably, the values from the data changed.


## Supervised Analysis

The Supervised method is an even more interesting analysis which directly is related to AI data-based learning algorithms. In this case, I have used Naive Bayes Clustering to make a Supervised Analysis. For a Supervised Analysis, the same data and clearing-procedure were undertaken. The Precision Score indicates the proportion of predicted positively labelled samples to be in reality positive labels. There is only one value 1, all the others are very close to 0 - that is a bad result. The Accuracy Classification Score shows to which extent the predicted labels are the same as the true labels corresponding to the same sample. A score of 0.15 is also an unpleasant result, where 1 is desired. The Recall Score shows how the clustering algorithm could predict all the positive samples. There is only one ideal score of 1, others are unsatisfying results. The F1-score is the mean value between the Precision Score and The Recall Score. All of the results are closer to 0 than to 1. The matrix also doesn't show a sign of successful clustering. To conclude, the clustering went badly.


## Results

There are no indicators of good clustering except for two scores. More tests should be run and other dataset values should be tested to achieve satisfying results. In overall, it was a great experience, even thought, the main goal of mine wasn't achieved. Next time, I will defiantly have better results. The topic of video game industry is infinite and the Data provided here could be used for more extensive analysis.
