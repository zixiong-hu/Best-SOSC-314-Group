# SOSC 314 Research Project
This project aims to analyze Clash Royale reviews from the Google Play Store and use text as data methods to understand the motivation behind good and bad reviews. Our motivation to research Clash Royale comes from the app's relevance to our demographic and we hope our findings on this app can serve as inspiration for companies looking to improve their apps. Each week of this 7 week class, we will make progress on the project until we exhaust our methods for analyzing this data.
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

# Google Colaboratory
https://colab.research.google.com/drive/1r0AIoHe4iQhcHq2k0ITj3KAilpcaQu9t?usp=sharing

# Planned Methods
* Sentiment Analysis
* Machine Learning Analysis
* Bag-of-Words Model

# Topic Model
We created topic modles on a 250k sample of both the positive and negative reviews. A positive review was defined as a review with a score of 3 stars or higher assigned to it. A negative review was defined as a review with a score of 2 stars or lower assigned to it. Both topic models showed a significant demand around the game's balance and fixing specific aspects of the game. The negative reviews topic model went more into depth about specific aspects that needed to be fixed, such as connectivity issues, matchmaking, and game balance isseus arising from certain cards and the monetization schemes.
