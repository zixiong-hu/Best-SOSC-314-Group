# SOSC 314 Research Project
This project aims to analyze Clash Royale reviews from the Google Play Store and use text as data methods to understand the motivation behind good and bad reviews. Our motivation to research Clash Royale comes from the app's relevance to our demographic and we hope our findings on this app can serve as inspiration for companies looking to improve their apps. Each week of this 7 week class, we will make progress on the project until we exhaust our methods for analyzing this data.

Final Project Report: 

## Authors
**Zixiong Hu and Matthew Banko**
# Research Question
What are the primary factors behind a good/bad review of the popular mobile game Clash Royale?
# Data Source
We will use the Google Play Store for review data. The dataset can be found here (https://drive.google.com/file/d/1nlbmyhJU6A5Uu5pmJoR7VcBj5_-XobwB/view?usp=sharing).
# Dataset Information
review_id - This is Google's unique id assigned to every review.

content - This is the review description containing the words that will be analyzed.

score - This is the star rating assigned to the review.

at - This is the time the review was created at.

likes - This is the number of likes a review has received.

appversion - This is the app's version at the time the review was submitted.

# Planned Methods
* Sentiment Analysis
* Machine Learning Analysis
* Bag-of-Words Model

# Dataset Used
Our full dataset contains around 2 million reviews with around 1.7 million reviews at 3 stars or above and around 400k reviews at 2 stars or below. Due to RAM and processing constraints, we are unable to utilize this dataset in its entireity. Where possible, we try to utilize a random sample of 500k reviews from this full dataset. In our analysis with trigrams and bigrams, we were only able to analyze with a sample of 100k reviews because of RAM constraints.

# Dataset Description
For each review, we collected a unique ID, textual content, score (1–5), timestamp, number of likes, and app version, excluding personal identifiers to avoid unnecessary data collection. The review text serves as the core analytical variable, while scores, time, likes, and app version allow us to examine trends across updates and over time. Initial descriptive statistics show an overall mean score of 4.19, but a sharp decline in more recent reviews (2025–2026), which average 3.24 compared to 4.23 for older reviews, suggesting a shift in player sentiment.

![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/bbda98bf77488c9ae64bab75b079581f80396cd6/Graphs%20and%20Results/All%20Review%20Score%20Histogram.png)

For preprocessing, we removed English stop words and other low-information grammar terms that dominated early word frequency results. Reviews were categorized as positive (score ≥ 3) or negative (score ≤ 2), and word frequency histograms were generated separately for each group to explore differences in language use. We believe that single words alone are insufficient to capture some meaningful opinions. As a result, we will apply n-gram models and dictionary-based approaches to capture multi-word phrases. We will assess whether numerical scores accurately reflect expressed opinions and to identify recurring themes driving player sentiment. Then, we will analyze the content of these reviews to determine pertinent features of positive and negative opinions of Clash Royale. Our hope is that game developers can use this case study to guide their efforts in improving their games.

![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/614b6b2a846354489a007c324ac961042b1bdd1c/Graphs%20and%20Results/Top%2020%20Words%20in%20Positive%20Reviews.png)
![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/614b6b2a846354489a007c324ac961042b1bdd1c/Graphs%20and%20Results/Top%2020%20Words%20in%20Negative%20Reviews.png)
# Lexicon Analysis
We used the natural language toolkit (NLTK)'s opinion_lexicon from nltk_corpus to analyze the lexical content of a random sample of 500k reviews. We wanted to predict the rating of a review based on the content of the review. We considered reviews with more positive words than negative words a positive review while reviews with more negative words than positive words were considered negative reviews. We then compared this result with the actual ratings of each review and found that our lexical approach classified around 67.8% of the reviews correctedly according to our definition. 

![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/b63d23f3e0e527d1d102cb5be71ca38d46ddf863/Graphs%20and%20Results/Lexicon%20Analysis%20Result.png)

# Logistic Regression Analysis
For our logistic regression analysis, we used a sample of 50k positive reviews and 50k negative reviews to ensure that our model was not more inclined towards a certain classification simply because of the proportion of the reviews it was trained on. We also sensitized for a couple of pre-processing decisions such as for removing numbers, inclusion/exclusion of English stop words, and changing the min_df/max_df, experimenting with various combinations of these pre-processing decisions. The most impactful change was a 4% decrease in accuracy when raising the min_f to 0.01 and lowering the max_df to 0.8. However, overall these changes had very little effect on our model's accuracy and F1 scores, and we ultimately settled on pre-processing with simply setting a min_df of 0.001 and max_df of 0.9. 

![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/27b4d81384baba732336c81ca240dbaeb205ebe4/Graphs%20and%20Results/Logistic%20Regression%20Report.png)

We also extracted the most influential positive and negative indicators in our logistic regression ranked by the coefficient value assigned to each word.

![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/27b4d81384baba732336c81ca240dbaeb205ebe4/Graphs%20and%20Results/Positive%20and%20Negative%20Coefficeints%20Logistic%20Regression.png)

In comparison to previous models (such as our unigrams and trigams), this proved most effective in presenting meaningful information: although there are still some relatively useless terms (such as "awesome" or "garbage") which do not convey much specific information, we see echoed complaints about the game's monetization, balancing, and cheating, and positive commentary on the game's addictive and entertaining nature. 

## Temporal Logistic Regression Analysis
In an attempt to narrow down the factors leading to a positive or negative review, we used the natural experiment of game updates to categorize reviews and compare the differences in a logistic regression model. We had four main categories in our test. A pre-2021 category was set up as that was the time period before Champions were introduced. A 2021-2023 category was set up for the time period where Champions were the major addition to the game. A 2023-2025 category was set up for the time period where Card Evolutions were the major addition to the game. A 2025 category was set up for the time period where Heroes were the major addition to the game. These are the coefficients for the logistic regression on each category in order of Pre-2021 to 2025.

![](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/89f937972e894b573b372e9ce6b0dec6a8442784/Graphs%20and%20Results/Pre-2021%20Coefficients.png)
![](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/89f937972e894b573b372e9ce6b0dec6a8442784/Graphs%20and%20Results/2021-2023%20Champions%20Coefficients.png)
![](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/89f937972e894b573b372e9ce6b0dec6a8442784/Graphs%20and%20Results/2023-2025%20Evos%20Coefficients.png)
![](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/89f937972e894b573b372e9ce6b0dec6a8442784/Graphs%20and%20Results/2025%20Post%20Hero%20Coefficients.png)

The most notable finding from these charts is the increasingly significance of concepts relating to the monetization scheme of the game. It appears that the monetization scheme becomes an ever more significant factor in negative reviews as the game recieves additional updates. This also tracks with our findings that more recent reviews have a much lower average rating compared to all reviews of the game.
# Random Forest Model
In addition to a logistic regression, we also ran a random forest model on our data, which we wanted to use to compare to our logistic regression. We were particularly interested in the ability to determine which words were most influential to the model in a random forest. We found the model performed similarly to our logistic regression model, but its influential words were not as interesting and meaningful compared to the logistic regression.

![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/27b4d81384baba732336c81ca240dbaeb205ebe4/Graphs%20and%20Results/Random%20Forest%20Report.png)

Influential words in Random Forest:

![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/beec56bfac37190f1c41c435875785e5e7417f48/Graphs%20and%20Results/Random%20Forest%20Coefficients.png)

# Topic Model
We created topic modles on a 250k sample of both the positive and negative reviews. A positive review was defined as a review with a score of 3 stars or higher assigned to it. A negative review was defined as a review with a score of 2 stars or lower assigned to it. Both topic models showed a significant demand around the game's balance and fixing specific aspects of the game. The negative reviews topic model went more into depth about specific aspects that needed to be fixed, such as connectivity issues, matchmaking, and game balance isseus arising from certain cards and the monetization schemes.

![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/8a38d0c317f73d57a57ef38e0c24e9e213afd726/Graphs%20and%20Results/Postive%20Topic%20Model%20Topics%20(df_min%20%3D%2050).png)
![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/8a38d0c317f73d57a57ef38e0c24e9e213afd726/Graphs%20and%20Results/Negative%20Topic%20Model%20Topics%20(df_min%20%3D%2050).png)

# Fightin' Words
Using the fightin' words method, we analyzed the words that differentiate positive and negative reviews. Our results from the fightin' words method largely confirm and support our existing findings. Positive reviews were differentiated by their mention of the game's addictive nature, the strategy involved in the game, and matchmaking. Negative reviews were differentiated by their mention of the game's monetization scheme, balancing, and matchmaking system. 

![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/44fb52f40e381048e386af88d5004bd2d3db5a1d/Graphs%20and%20Results/Fightin%20Words%20positive%20words%20with%20stop%20words.png)
![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/44fb52f40e381048e386af88d5004bd2d3db5a1d/Graphs%20and%20Results/Fightin%20Words%20negative%20with%20stop%20words.png)

In addition, we also conducted the fightin' words method on a filtered sample that had stop words removed. We found that the sample retained nearly the same results, except that it was easier to read with the removal of stop words.

![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/a555c2efd53649c328518c2ee44eb39e0a5beb8d/Graphs%20and%20Results/Fightin%20Words%20positive%20without%20stop%20words.png)
![alt text](https://github.com/zixiong-hu/Best-SOSC-314-Group/blob/a555c2efd53649c328518c2ee44eb39e0a5beb8d/Graphs%20and%20Results/Fightin%20Words%20negative%20without%20stop%20words.png)

# Reproducibility
## Environment
- Python 3.12
- pandas 3.0.1
- numPy 2.4.2
- matplotlib 3.10.8
- scikit-learn 1.8.0
- nltk 3.9.1
- pyLDAvis 3.4.1
- FightingWords

Tested on Google Colab between Janaury and Feburary 2026
## Data Collection
Data collection was done using the google-play-scraper package. The package allows for any Google Play Store app's review page to be scraped for its content and metadata. Below is the code used to scrape and save the data into a csv for permenant usage.
```
from google_play_scraper import Sort, reviews
MAX_REVIEWS = float("inf")  # scrape until exhaustion
all_reviews = []
token = None

while True:
    batch, token = reviews(
        'com.supercell.clashroyale',
        continuation_token=token
    )

    if not batch:
        break

    all_reviews.extend(batch)

    if len(all_reviews) >= MAX_REVIEWS:
        break



    # polite delay to reduce throttling
    time.sleep(0.2)

file_path = "/content/drive/MyDrive/clash_royale_reviews.csv"
df = pd.DataFrame(all_reviews)

df = df.rename(columns={
    "reviewId": "review_id",
    "thumbsUpCount": "likes"
})

df["at"] = pd.to_datetime(df.get("at"), errors="coerce")

desired_cols = [
    "review_id",
    "content",
    "score",
    "at",
    "likes",
    "appVersion"
]

df = df[[c for c in desired_cols if c in df.columns]]

df.to_csv(file_path, index=False)
```
## Jupyter Notebooks
The simplest way to reproduce our results is to run our juypter notebooks stored in the CoLab Weekly Updates folder of our Github page. The file path and certain dependencies may need to be altered for your specific environment. To follow the temporal order of our project, go in the order of
1. Clash Royale Reviews Analysis
2. Clash_Royale_Data
3. Week 3 Data Analysis
4. Clash_Royale_Operationalization
5. Clash_Royale_Week_5
6. Clash_Royale_Topic_Models
7. Clash_Royale_Week_6

