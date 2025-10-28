# Restaurant Review Sentiment Analysis

This project is a classic Natural Language Processing (NLP) task focused on sentiment analysis. The goal is to build and evaluate several machine learning models to classify 1,000 restaurant reviews as either positive or negative.



---

##  Aim
The primary aim of this project is to create a complete NLP pipeline, including:
* Performing **Exploratory Data Analysis (EDA)** on text data.
* **Cleaning and preprocessing** raw text for machine learning.
* Implementing and comparing two different **feature extraction** techniques (Bag of Words and TF-IDF).
* Building, training, and evaluating three different **classification models** to find the best performer.

---

##  Dataset
The dataset is a `.tsv` file (`Restaurant_Reviews.tsv`) containing 1,000 reviews.
* **`Review`**: The raw text of the review.
* **`Liked`**: The sentiment label (1 for Positive, 0 for Negative).
* The dataset is perfectly balanced, with 500 positive and 500 negative reviews.

---

##  Project Workflow

### 1. Exploratory Data Analysis (EDA)
I began by analyzing the dataset to uncover patterns. This included:
* Plotting the **class distribution** (50/50 balance).
* Analyzing **review length** (word count and character count) to see if it correlated with sentiment.



### 2. Text Preprocessing (Data Cleaning)
To prepare the text for modeling, I created a "corpus" by applying the following steps to each review:
1.  **Remove Non-alphabetic Characters:** Used `re.sub` to remove all punctuation, numbers, and symbols.
2.  **Lowercase:** Converted all text to lowercase.
3.  **Tokenize:** Split the text into a list of words.
4.  **Remove Stopwords:** Filtered out common English stopwords (e.g., "the", "is", "a") using NLTK.
5.  **Stemming:** Reduced words to their root form (e.g., "loved", "loving" -> "love") using NLTK's `SnowballStemmer`.
6.  **Rejoin:** Joined the cleaned tokens back into a single string, ready for vectorization.

### 3. Feature Extraction
I converted the cleaned text corpus into numerical vectors using two different methods to compare their effectiveness:

* **Bag of Words (BoW):** Created using `sklearn.feature_extraction.text.CountVectorizer`. This represents each review based on the *count* of each word it contains.
* **TF-IDF (Term Frequency-Inverse Document Frequency):** Created using `sklearn.feature_extraction.text.TfidfVectorizer`. This represents each review by *scoring* words based on their importance, giving higher weight to words that are frequent in one review but rare across all reviews.

### 4. Model Building
I trained and evaluated three different supervised machine learning models. Each model was tested with *both* the Bag of Words and TF-IDF features to find the best-performing combination.

**Models Used:**
1.  **Multinomial Naive Bayes (`MultinomialNB`):** A fast and effective baseline model that works very well with text count data.
2.  **Logistic Regression:** A robust linear model that is highly effective and interpretable for binary classification tasks.
3.  **Linear Support Vector Classifier (`LinearSVC`):** A powerful SVM model that is often a top performer for text classification due to its ability to handle high-dimensional, sparse data.

(For a detailed breakdown of model performance and evaluation metrics, please see the `results.md` file.)

---

## 🔧 Libraries & Tools Used
* **Pandas:** For loading and managing data.
* **NLTK:** For text preprocessing (stopwords, stemming).
* **re (Regex):** For cleaning text.
* **Scikit-learn (`sklearn`):** For feature extraction, models, and evaluation.
* **Matplotlib / Seaborn:** For data visualization.
* **WordCloud:** For EDA visualization.

# Results
##  Final Model Comparison: BoW vs. TF-IDF

I ran all three classifiers using both Bag of Words (BoW) and TF-IDF feature extraction, evaluating each with 5-fold cross-validation.

### Bag of Words (BoW) Results

| Model | Average Accuracy | Standard Deviation |
| :--- | :--- | :--- |
| **LinearSVC (SVM)** | **80.20%** | **&plusmn; 1.78%** |
| Logistic Regression | 79.90% | &plusmn; 1.66% |
| Multinomial Naive Bayes | 78.20% | &plusmn; 1.29% |

### TF-IDF Results

| Model | Average Accuracy | Standard Deviation |
| :--- | :--- | :--- |
| **Logistic Regression** | **80.50%** | **&plusmn; 1.38%** |
| LinearSVC (SVM) | 79.50% | &plusmn; 1.26% |
| Multinomial Naive Bayes | 78.20% | &plusmn; 2.11% |


##  Overall Conclusion

This experiment shows that both Bag of Words and TF-IDF are very effective, with all models performing within a tight ~2% range.

Interestingly, while **Logistic Regression** saw a slight boost from TF-IDF (reaching a top accuracy of **80.50%**), the **LinearSVC** model actually performed best with the simpler **Bag of Words** (at **80.20%**).

This demonstrates that for this specific dataset, the raw counts of words (BoW) are a highly effective and robust signal for sentiment, and the additional complexity of TF-IDF does not provide a significant advantage.