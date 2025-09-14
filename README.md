# 🎬 YoutubeTrailer_ML – Final Project

## 📌 About this repository  
- This is a project that analyzes **YouTube movie trailers** using exploratory data analysis and machine learning.  
- The objective of this project is to apply data analysis and machine learning tools as part of a course assignment. The resulting model and insights are intended purely for academic and practical learning purposes.

The workflow includes:  
1. **EDA** - understanding the dataset.  
2. **Data cleaning and consolidation** - clarifying hypotheses.  
3. **Feature selection & machine learning** - predictive modeling.  

---

## 📂 structure 
- **data/**
  - **raw/**
    - movies_youtube_sentiments.csv
  - **processed/**
    - movies_youtube_sentiments_clean.csv  

- **notebooks/**
  - AnalysisYoutubeTrailer_I.ipynb              📒 Initial EDA  
  - AnalysisYoutubeTrailer_II.ipynb             📒 Consolidated EDA and documentation  
  - AnalysisYoutubeTrailer_III.ipynb            📒 ML model feature selection + training  
  - AnalysisYoutubeTrailer_Final.ipynb          📒 Unified notebook (I + II + III)  

- **docs/**
  - Readme_I.md  
  - Readme_II.md  
  - Readme_III.md  

- **requirements.txt**  
---

## 📌 Dataset  

- **Dataset:** `movies_youtube_sentiments.csv`  
- **Link:** [Kaggle – Movies YouTube Trailers and Sentiment](https://www.kaggle.com/datasets/dineshvasired/movies-youtube-trailers-and-sentimentdinesh-dinesh)  
- **Size:** - 5,000 rows, 10+ columns   
- **Main variables:**  
  - `genre` → movie genre  
  - `rating` → movie rating (e.g., PG-13, R)  
  - `budget` → production budget (USD)  
  - `positive`, `neutral`, `negative` → sentiment counts from YouTube comments  

---

## 📌 Project Stages  
###  Part I – Data Exploration  
- Inspected dataset structure, missing values, and duplicates.  
- Performed visualizations: **genre distribution**, **ratings**, and **sentiment counts**.

#### 1. Sentiment Feature Engineering  
- Transformed the original `sentiment_scores` column, which were in string format, into a structured dictionary called `sentiment_dicts`.  
- Extracted key values,`positive`, `neutral`, `negative`, and created separate sentiment columns.  

#### 2. Derived Metrics  
I created additional variables to enrich sentiment analysis:  

- **total_comments**: sum of positive, neutral, and negative comments per video.  
  *→ Provides the overall engagement volume.*  

- **positive_ratio**: proportion of positive comments over the total.  
  *→ Helps measure positivity share.*  

- **emotional_balance**: difference between positive and negative comments.  
  *→ Shows the emotional tilt.*  

- **favorability_level**: categorical classification of videos based on `positive_ratio` (`very low`, `low`, `medium`, `high`, `very high`).  
  *→ Useful for grouping and interpreting sentiment levels.*  

### 3. Categorical Encoding: `genre` and `rating`  
- The columns `genre` and `rating` originally contained text categories, e.g., *Comedy*, *Action*, *PG-13*, *R*.  
- To enable analysis and visualization, I transformed them into **dummy variables** (0/1) using `pandas.get_dummies()`.  

#### Example  
If a video belongs to the *Comedy* genre:  
- `genre_Comedy = 1`  
- All other `genre_*` columns = 0  

#### Why does this helps?  
- Facilitates comparisons across genres and ratings  
- Allows filtering by content type  
- Enables visualizations and numerical analysis with categorical data  

---

### Sentiment Distribution  

#### 📊 1. Distribution of Favorability `positive_ratio`  
<img width="695" height="471" alt="image" src="https://github.com/user-attachments/assets/c1552c6f-fcb4-4773-bf0b-84cc8146335d" />  

I analyzed the distribution of `positive_ratio` to understand how trailers were emotionally received.  

- **X-axis**: proportion of positive comments (0 to 1)  
- **Y-axis**: frequency of trailers  

  ► **Key insights**:  
- Most trailers cluster around 0.4, meaning less than half of comments are positive.  
- A smaller group shows very low favorability (0.1–0.2).  
- Very few reach extremely high favorability levels (>0.7).  

This suggests that most trailers receive a **mixed or moderately favorable** emotional response.  

---

#### 📊 2. Genre Frequency (`genre`)  
<img width="850" height="517" alt="image" src="https://github.com/user-attachments/assets/fcc3185a-4967-4ecd-9dbc-f4160b4d10de" />  

I analyzed the number of movies per genre in the dataset.  

  ► **Key insights**:  
- **Action**, **Comedy**, and **Drama** dominate the dataset.  
- Genres like **Crime**, **Horror**, and **Biography** are moderate.  
- Others (**Mystery**, **Sci-Fi**, **Thriller**, **Fantasy**, **Romance**) appear only a few times, limiting statistical significance.  

This imbalance indicates the dataset is skewed toward mainstream genres, which could affect model generalization.  

---

#### 📊 3. Average Positive Comments by Genre  
<img width="846" height="517" alt="image" src="https://github.com/user-attachments/assets/1b08bd4c-12d1-400f-8f9e-a7bcb07a2240" />  

I compared the average `positive_ratio` across genres.  

  ► **Key insights**:  
- **Romance** has the highest average positivity.  
- **Comedy** and **Biography** also perform well, with above-average positivity.  
- **Horror** and **Sci-Fi** show lower positivity. 
- Audience sentiment varies significantly by genre, which is valuable context for prediction.  

---

### Tentative Conclusions.  

- The **imbalance in genre representation** suggests categorical variables like `genre`, `rating` may require balancing or weighting strategies in classification.  
- Since most trailers concentrate around a **moderate favorability ratio 0.4**, predicting extremes, very low/high, may be harder.  
- Derived metrics (`positive_ratio`, `emotional_balance`, `favorability_level`) are strong candidate predictors.  
- Genre-level patterns, Romance higher positivity, Horror lower, indicate potential **interactions between genre and sentiment variables**.  

---

## 📌 Part II – Consolidation and Hypotheses  
- This section explores patterns in the dataset to generate insights, test hypotheses, and propose predictive models.

  ► **Tasks**
-  Cleaned dataset and stored it in `processed/`.  
- Defined research questions and hypotheses.  
- Explored relationships between sentiment ratios, budget, and genres.  
- Proposed possible supervised models.

   ► **Research Questions / Hypotheses**
1. Do trailers with higher positive comment counts or proportions tend to achieve greater favorability?  
2. Does the movie genre influence the reception of the trailer?  
3. Is there a relationship between the movie’s budget and favorability on YouTube?  
4. Is the movie’s rating associated with the audience’s emotional response?  

---

### 📊 Distribution of Sentiment Comments
- Most trailers accumulate a large number of **positive and neutral comments**, while **negative comments are less frequent**.  
- This suggests an overall bias toward neutral/positive engagement on YouTube.  
<img width="831" height="478" alt="image" src="https://github.com/user-attachments/assets/2f7876b8-23f1-4229-aba8-af05e5a9836c" />

---
### 📊 Positive Comments by Genre
- Genres like **Action, Drama, and Animation** show higher medians of positive comments.  
- **Comedy** is highly variable: some trailers receive very high positivity, while others receive very few comments.  
- This indicates that **genre moderates audience response** but does not guarantee consistent favorability.  
<img width="850" height="517" alt="image" src="https://github.com/user-attachments/assets/b301bc41-9921-4f63-90b9-562303dd8647" />

---

### 📊 Budget vs. Positive Comment Ratio
- There is **no clear correlation** between budget and proportion of positive comments.  
- Low and medium-budget films can achieve high favorability.  
- High-budget productions do not necessarily guarantee stronger audience reception.  
<img width="691" height="471" alt="image" src="https://github.com/user-attachments/assets/3527f9f5-d356-4c96-b669-8b99ac0b3929" />

---

### Insights-Based Recommendations
- **Action** and **Comedy** trailers tend to gather more positive comments and engagement.  
- **Budget size is not a predictor** of higher favorability. Marketing and audience alignment may be more critical.  

---

### Learning Type and Proposed Models
This is framed as a **supervised learning problem**, where the goal is to predict `favorability_level`.  

**Candidate models:**  
- Logistic Regression  
- Decision Tree  
- Random Forest Classifier  


--- 

## 📌 Part III – Feature Selection & ML Model  


###  Target Definition:`favorability_ratio` & `favorability_level_3`
- Created a `favorability_ratio` combining positive, neutral, and negative comments.  
- Neutral comments were weighted at **0.25** to avoid them dominating the metric and to give more influence to positive/negative reactions.  
- The continuous metric was transformed into a balanced categorical target,`low`, `medium`, `high`, using **qcut**, ensuring similar group sizes.  
<img width="630" height="470" alt="image" src="https://github.com/user-attachments/assets/d6e8f68e-c1dd-4a1f-a492-516783cbc26c" />

---
###  Feature Selection
- **Chi2 test** identified quantitative and sentiment-related features as most relevant:  
  - `gross`, `budget`, `votes`  
  - `positive`, `neutral`, `negative`, `total_comments`  
  - `runtime`  
- **ANOVA F-test** confirmed the importance of sentiment variables, while also highlighting some genres.  
- **Decision**: genre dummies were excluded to avoid bias, keeping the **top 8 numeric/sentiment features**.

---

###  Model Training
I used three supervised classification algorithms with `favorability_level_3` as target:  

1. **Decision Tree**  
   - Accuracy ≈ 0.70  
   - Performs well on `low` and `medium` classes, but weaker on `high`.
     <img width="528" height="393" alt="image" src="https://github.com/user-attachments/assets/a2af5984-f02c-4fd1-95f0-c09242b30402" />


2. **Logistic Regression**  
   - Accuracy improved from 0.73 → 0.84 with more iterations (`max_iter=5000`).  
   - Excellent recall for `low` and `medium`, but still weaker on `high` (~65%).  

3. **Random Forest**  
   - Accuracy ≈ 0.80  
   - More **balanced performance** across classes.  
   - Recall for `high` = 0.72, better than Decision Tree and Logistic Regression.  

---

### Results
- **Logistic Regression (5000 iter)**: highest global accuracy (0.84), but unbalanced across classes.  
- **Random Forest**: slightly lower accuracy (0.80) but more consistent across all classes.  
- **Decision Tree**: simpler but less effective.  

---

### 📌 Conclusions
- **EDA (Part II)** provided context on variables like genre and budget, but feature selection revealed that **sentiment metrics and engagement variables** are stronger predictors.  
- **Random Forest** was the most balanced model, offering good precision and recall across all target classes, even if Logistic Regression achieved a slightly higher accuracy.  
- The project highlights that **audience sentiment variables** are crucial to predicting favorability, while genre and budget alone are not strong predictors.  

► This makes Random Forest a good candidate for practical applications, while Logistic Regression could be useful as a lightweight baseline.  

---

## 📌 Results  

- In the initial EDA, variables such as **genre** and **budget** were explored to build context and hypotheses.  
- After applying **dimensionality reduction**, other dataset features proved to be more relevant predictors.  
- Three classifiers were trained: **Decision Tree, Logistic Regression, and Random Forest**.  
- The classification model achieved **~70–75% accuracy** in predicting trailer favorability.  
- Feature selection improved interpretability by highlighting the **10 most predictive variables**.  
- **Random Forest** achieved the best performance, with a balanced trade-off between precision and recall, and an **accuracy close to 80%**.  
- The project served as a **practical exercise** in feature selection, model training, and evaluation, with results intended for academic purposes only.  
 

---

## ⚙ Installation and Usage

 ### 1. Clone the repository
   git clone https://github.com/JotaNota/YoutubeTrailer_ML.git
   cd YoutubeTrailer_ML
   git checkout main

 ### 2. Create and activate a virtual environment
     python -m venv venv

   ####  macOS/Linux
     source venv/bin/activate
   #### Windows
     venv\Scripts\activate

 ### 3. Install dependencies
   pip install -r requirements.txt

 ### 4. Run the notebooks
   jupyter notebook
