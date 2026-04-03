# 📊 Thai Broker Services Sentiment Analysis on Pantip

This repository presents a complete data pipeline and machine learning model designed to analyze Thai public opinions regarding financial broker services, based on discussions from the web forum Pantip.com. 

The primary objective of this project is to process complex Thai text, categorize the topics being discussed, and classify the underlying sentiment (Positive, Neutral, or Negative) of user comments to extract actionable data insights.

## 🛠️ Tools & Libraries Used

* **Data Collection:** `Selenium`, `webdriver_manager`
* **Data Processing:** `pandas`, `numpy`
* **Thai NLP:** `PyThaiNLP` (newmm engine), `nltk`, `emoji`, `re`
* **Machine Learning:** `scikit-learn` (TF-IDF, Logistic Regression), `imblearn`
* **Data Visualization:** `matplotlib`, `wordcloud`

---

## ⚙️ Project Workflow

The system is structured into four main phases to transform raw forum data into structured insights. 

### 1. Data Collection (Web Scraping)
We utilized **Selenium** to automate a web browser in headless mode to navigate and extract data from targeted Pantip forum threads. The scraper collected various data points including thread titles, tags, usernames, and the main comment bodies. The raw dataset consists of 1,327 comments.

### 2. Text Preprocessing
Processing Thai text from internet forums presents unique challenges due to the lack of word boundaries (spaces) and the frequent use of informal language. Our text cleaning pipeline involves:
* **Demojizing:** Converting emojis into descriptive text (using the `emoji` library) to ensure the emotional context is not lost before removing special characters.
* **Noise Removal:** Stripping out unnecessary punctuation, URLs, mentions (@), and non-alphanumeric characters.
* **Tokenization:** Segmenting sentences into individual words using the `newmm` dictionary-based algorithm from `PyThaiNLP`.
* **Stopwords Removal:** Filtering out common Thai conjunctions and filler words that do not carry sentimental weight.

### 3. Topic Categorization
Before analyzing sentiment, we grouped the comments into specific areas of interest using a rule-based approach. By defining sets of targeted keywords, the system classifies each comment into one of five main categories:
1.  **System Issues** 
2.  **Fees** 
3.  **Service** 
4.  **Trading** 
5.  **Others** 

### 4. Sentiment Classification
* **Handling Imbalanced Data:** The initial dataset had an unequal distribution of sentiments. We applied an **Under-sampling** technique to balance the Positive, Neutral, and Negative classes (reducing them to 303 samples each) to prevent model bias towards the majority class.
* **Feature Extraction:** We used **TF-IDF** (`ngram_range=(1,3)` and `max_features=5000`) to convert the tokenized text into numerical vectors that the machine learning model can process.
* **Model Training:** A **Lasso Logistic Regression (L1 Penalty)** was implemented for the classification task. The L1 penalty was specifically chosen because it performs automatic feature selection, effectively ignoring irrelevant words in the highly sparse text data and helping to prevent overfitting.

---

## 📈 Results & Key Findings

**Model Performance:**
* **Overall Accuracy:** **73.08%** on the test set.
* **F1-Score (Positive):** 0.84 (The model is highly effective at identifying positive feedback).
* **F1-Score (Negative & Neutral):** 0.67

**Data Insights:**
* **Most Discussed Topic:** "Trading" was the most frequently discussed topic among users, accounting for 62% of the total comments.
* **Sentiment Correlation:** Comments related to **"System Issues"** showed a strong correlation with **Negative** sentiment. Conversely, comments discussing **"Service"** tended to lean heavily towards **Positive** sentiment.

---
