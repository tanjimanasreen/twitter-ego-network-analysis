# Dataset Glossary & Feature Dictionary

This document provides a comprehensive reference for the data structures and engineered features used in the **`twitter-ego-network-analysis`** study.

---

## 1. Cohort Structure

The research pipeline investigates **10 distinct user groups** (9 self-reported mental health conditions and 1 control group):

| Cohort | Label Code | Description |
| :--- | :--- | :--- |
| **ADHD** | `Adhd_eng` | Attention Deficit Hyperactivity Disorder cohort |
| **Anxiety** | `Anxiety_eng` | Generalized anxiety disorder cohort |
| **ASD** | `Asd_eng` | Autism Spectrum Disorder cohort |
| **Bipolar** | `Bipolar_eng` | Bipolar disorder cohort |
| **Control** | `Control_eng` | Baseline control group (active users without self-reported diagnoses) |
| **Depression** | `Depression_eng`| Clinical depression cohort |
| **Eating Disorders** | `Eating_eng` | Eating disorder cohort |
| **OCD** | `Ocd_eng` | Obsessive-Compulsive Disorder cohort |
| **PTSD** | `Ptsd_eng` | Post-Traumatic Stress Disorder cohort |
| **Schizophrenia** | `Schizophrenia_eng`| Schizophrenia cohort |

---

## 2. Feature Schema & Column Definitions

The data extraction pipeline processes longitudinal tweet histories and extracts user-level, linguistic, temporal, and network interaction features.

| Field Name | Type | Description |
| :--- | :--- | :--- |
| `tweet_id` | String | Unique identifier of the tweet |
| `day` | String | Day of the week when the tweet was posted |
| `time` | String | Timestamp (HH:MM:SS) of the tweet |
| `tweet_text` | String | Original raw text content of the tweet |
| `clean_tweet_lemma` | String | Lemmatized and normalized text |
| `tweet_favorite_count` | Integer | Number of likes/favorites received |
| `tweet_retweet_count` | Integer | Number of times the tweet was retweeted |
| `tweet_quote_count` | Integer | Number of quote tweets |
| `tweet_reply_count` | Integer | Number of direct replies received |
| `tweet_source` | String | Client used to post (e.g., Twitter Web App, Twitter for Android) |
| `user_id` | String | Unique identifier of the Twitter user *(anonymized in public releases)* |
| `user_screen_name` | String | Twitter handle/screen name *(redacted in public releases)* |
| `user_description` | String | User biography text *(redacted in public releases)* |
| `user_followers_count` | Integer | Number of followers at the time of data collection |
| `user_friends_count` | Integer | Number of accounts the user follows (following/friends count) |
| `user_listed_count` | Integer | Number of public lists containing the user |
| `user_statuses_count` | Integer | Lifetime tweet count of the account |
| `text_preprocessed` | String | Cleaned text with stopwords, emojis, URLs, and hashtags removed |
| `text_hashtags` | Array[String] | List of hashtags extracted from the tweet |
| `hashtags_count` | Integer | Total count of hashtags in the tweet |
| `text_handles` | Array[String] | Mentioned user handles (`@mentions`) in the tweet |
| `handles_count` | Integer | Total count of mentioned user handles in the tweet |
| `text_emojis` | Array[String] | Unicode emojis extracted from the tweet text |
| `emojis_count` | Integer | Total count of emojis in the tweet |
| `text_asp_preprocessed` | String | Preprocessed text for Aspect-Based Sentiment Analysis (ABSA) |
| `aspect_sentiment` | Array[Dict] | Aspect sentiment schema (`main_aspect`, `found_aspect`, `neg`, `neu`, `pos`, `compound`) |
| `text_sentiment` | Float | Compound VADER sentiment polarity score `[-1.0, +1.0]` |
| `text_preprocessed_freq` | Dict | Token frequency dictionary for preprocessed terms |
| `text_pv_freq` | Dict | Frequency of words matching the 10 Schwartz Personal Values: *Self-Direction, Stimulation, Hedonism, Achievement, Power, Security, Conformity, Tradition, Benevolence, Universalism* |
| `text_humour_freq` | Dict | Frequency of tokens matching humour lexicons (*not_funny, medium_funny, funny, super_funny*) |
| `text_sentiment_freq` | Dict | Frequency distribution of positive vs. negative lexical tokens |
| `text_emotion_freq` | Dict | Frequency of tokens matching 8 basic Plutchik emotions: *anger, anticipation, disgust, fear, joy, sadness, surprise, trust* |
| `text_personality_freq` | Dict | Token counts associated with Big-5 personality trait lexicons |
| `text_personality_score` | Dict | Computed OCEAN score weights: **O**penness, **C**onscientiousness, **E**xtraversion, **A**greeableness, **N**euroticism |
| `engagement_rate` | Float | Engagement ratio per user: `(favorites + retweets + replies) / followers` |
| `extended_reach` | Float | Percentage reach: `(retweets + likes + replies + quotes) / followers * 100` |
| `possible_impressions` | Float | Normalized impression estimate: `retweets / total_tweets * 100` |

---

## 3. Extracted Aggregated Analysis Features

For user-group and network-group statistical analysis ([notebooks/4_analysis_and_modeling.ipynb](notebooks/4_analysis_and_modeling.ipynb)), features are aggregated to the user level:

| Feature | Formula / Method | Description |
| :--- | :--- | :--- |
| `avg_tweets_per_day` | $\text{Total Tweets} / \text{Active Span (Days)}$ | Average tweeting frequency per day |
| `avg_tweet_favorite_count` | $\sum \text{Likes} / \text{Total Tweets}$ | Average likes per tweet |
| `avg_tweet_reply_count` | $\sum \text{Replies} / \text{Total Tweets}$ | Average replies per tweet |
| `avg_text_sentiment` | $\sum \text{Polarity} / \text{Total Tweets}$ | Average sentiment score |
| `avg_engagement_rate` | $\sum \text{Engagement} / \text{Total Tweets}$ | Average engagement rate |
| `avg_emojis_count` | $\sum \text{Emojis} / \text{Total Tweets}$ | Average emoji usage per tweet |
| `avg_tweet_retweet_count` | $\sum \text{Retweets} / \text{Total Tweets}$ | Average retweets per tweet |
| `most_active_period` | Mode of time bins | Categorical: *Morning (5:00-11:59)*, *Afternoon (12:00-16:59)*, *Evening (17:00-20:59)*, *Night (21:00-23:59)*, *Midnight (1:00-4:59)* |
| `most_active_day` | Mode of day of week | Most frequent day of activity (Monday through Sunday) |
| `user_group` | Target Label | Binary classification: `diagnosed` vs `control` |
| `o, c, e, a, n` | Mean lexical trait scores | Aggregated Big-5 personality trait measures |
