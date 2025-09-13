# 🎬 YoutubeTrailer_ML – Final Project

## 📌 About this repository  
This is a project that analyzes **YouTube movie trailers** using exploratory data analysis and machine learning.  
The objective of this project is to apply data analysis and machine learning tools as part of a course assignment. The resulting model and insights are intended purely for academic and practical learning purposes.

The workflow includes:  
1. **EDA** – understanding the dataset.  
2. **Data cleaning and consolidation** – clarifying hypotheses.  
3. **Feature selection & machine learning** – predictive modeling.  
4. **Final unified notebook** – combining all stages in one notebook.  

---

## 📂 structure - Part IV  
- **data/**
  - **raw/**
    - movies_youtube_sentiments.csv
  - **processed/**
    - movies_youtube_sentiments_clean.csv  

- **notebooks/**
  - AnalysisYoutubeTrailer_I.ipynb   📒 Initial EDA  
  - AnalysisYoutubeTrailer_II.ipynb  📒 Consolidated EDA and documentation  
  - AnalysisYoutubeTrailer_III.ipynb 📒 ML model feature selection + training  
  - AnalysisYoutubeTrailer_Final.ipynb 📒 Unified notebook (I + II + III)  

- **docs/**
  - Readme_Part_I.md  
  - Readme_Part_II.md  
  - Readme_Part_III.md  

- **requirements.txt**  
---

## 📌 Dataset  

- **Source:** `movies_youtube_sentiments.csv`  
- **Link:** [Kaggle – Movies YouTube Trailers and Sentiment](https://www.kaggle.com/datasets/dineshvasired/movies-youtube-trailers-and-sentimentdinesh-dinesh)  
- **Size:** ~5,000 rows, 10+ columns   
- **Main variables:**  
  - `genre` → movie genre  
  - `rating` → movie rating (e.g., PG-13, R)  
  - `budget` → production budget (USD)  
  - `positive`, `neutral`, `negative` → sentiment counts from YouTube comments  
  - `positive_ratio`, `emotional_balance` → engineered features  

---

## 📌 Project Stages  

###  Part I – Data Exploration  
- Inspected dataset structure, missing values, and duplicates.  
- Performed visualizations: genre distribution, ratings, and sentiment counts.  

### Part II – Consolidation and Hypotheses  
- Cleaned dataset and stored it in `processed/`.  
- Defined research questions and hypotheses.  
- Explored relationships between sentiment ratios, budget, and genres.  
- Proposed possible supervised models.  

### Part III – Feature Selection & ML Model  
- Applied feature selection (`SelectKBest`, chi2).  
- Trained classification model using `favorability_level` as target.  
- Evaluated model with accuracy and confusion matrix.  
- Documented conclusions from results.  

### Part IV – Unified Notebook  
- Combined all steps into a single notebook
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

## ⚙️ Installation and Usage  

1. Clone the repository:  
   ```bash
   git clone https://github.com/JotaNota/YoutubeTrailer_ML.git
   cd YoutubeTrailer_ML
   git checkout Part_IV_Merge
