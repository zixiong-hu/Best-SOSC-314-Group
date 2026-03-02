# Prerequisite Info
The file containing our review data was nearly 1GB in size. Ensure that there will be no hardware limiations before running this code.
## Requirements
- Python 3.12
- Pandas 
## Installation
```
npm install google-play-scraper
```
## Data Collection for Clash Royale
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
```
Using this, we were able to scrape up to 2.2 million reviews from the Google Play Store.
## Save into a csv file
```
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
This saves the scraped reviews into a csv file for permenant access.
