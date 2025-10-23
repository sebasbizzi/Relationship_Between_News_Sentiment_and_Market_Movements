# Project: Investigating the Relationship Between News Sentiment and Market Movements
**Author:** Sebastian Bizzi
**Date:** October 23, 2025

---
## 1. Project Goal & Context

Financial markets are influenced by countless factors, including the constant stream of news. This project aimed to rigorously investigate the potential relationship between the sentiment expressed in daily financial news headlines (sourced from The Guardian) and the short-term movements of a major stock market index (S&P 500).

The objective was to conduct a **proof-of-concept analysis** using 5 years of historical data to determine if a discernible link exists using common NLP and data analysis techniques.

---
## 2. Methodology & Tools

The analysis followed a structured workflow within Google Colab, using Python and key libraries:

* **Data Collection:**
    * Fetched 5 years of historical headlines from **The Guardian API** ('business' section) using `requests`.
    * Downloaded corresponding S&P 500 (`^GSPC`) daily data using `yfinance`.
* **Data Processing & Merging:**
    * Cleaned dates and aggregated daily headlines using **Pandas**.
    * Calculated daily market direction (1 for up, 0 for down) based on closing prices.
    * Merged news and market data by date into a final analysis DataFrame (`analysis_df`) containing 1253 trading days.
* **Feature Engineering & Analysis:**
    * **Sentiment Analysis:** Applied **NLTK VADER** to calculate a compound sentiment score for each day's aggregated headlines.
    * **Volume Analysis:** Calculated daily news volume (word count proxy).
    * **Topic Modeling:** Used **Scikit-learn (TF-IDF & NMF)** to identify 10 latent topics within the headlines.
* **Correlation Analysis:**
    * Compared average sentiment scores on market up vs. down days.
    * Compared average news volume on market up vs. down days.
    * Analyzed the percentage of market up-days associated with each dominant topic.
    * Analyzed the average sentiment score within each dominant topic.
* **Predictive Modeling:**
    * Trained a basic **Scikit-learn Logistic Regression** model using the daily sentiment score to predict the *next day's* market direction.

---
## 3. Key Findings & Conclusion

The iterative analysis yielded clear and consistent results:

1.  **Simple Metrics Lack Strong Signals:** Neither the aggregated daily sentiment score (-0.31 on down days vs. -0.28 on up days) nor the news volume showed a significant difference between market up and down days.
2.  **Topic Modeling Offers Nuance:** Certain topics showed a slightly stronger association with market direction (e.g., Topic 10/Crypto and Topic 2/Trade coincided more with up-days; Topic 6/Inflation slightly more with down-days). However, the sentiment *within* these topics did not show a simple predictive pattern.
3.  **Basic Prediction Fails:** The Logistic Regression model attempting to predict the next day's market direction based on today's sentiment achieved an accuracy of **49.80%**, failing to outperform a simple baseline (56.97%).

**Overall Conclusion:** This project demonstrates that extracting a reliable predictive signal for daily market movements solely from news headlines, even high-quality ones over a 5-year period, is highly challenging using common sentiment and topic modeling techniques applied at a daily aggregate level.

---
## 4. Strategic Recommendation

The key takeaway is that developing a valuable predictive tool requires moving beyond simple, aggregated metrics. Future efforts should focus on:

* **Advanced Feature Engineering:** Developing more sophisticated features (sentiment on specific entities, topic-specific volume, event detection).
* **Sophisticated Modeling:** Employing contextual NLP models tuned for finance and advanced time-series analysis.
* **Data Fusion:** Integrating news data with other market indicators.

This project successfully established a data pipeline, tested multiple hypotheses rigorously, and concluded that a more nuanced approach is necessary to capture the market's complex reaction to news.

---
## 5. Code

The complete Python code for this analysis can be found in the Google Colab Notebook file within this repository:
[`Relationship_Between_News_Sentiment_and_Market_Movements.ipynb`](./Relationship_Between_News_Sentiment_and_Market_Movements.ipynb)

