🍽️ Food Recommendation System with Hybrid Filtering

📌 Project Overview

This project is a submission for Dicoding’s Machine Learning Terapan - Submission 2. It aims to build a hybrid food recommendation system that combines Content-Based Filtering and Collaborative Filtering to help users discover foods based on both personal preferences and content similarity.

📊 Dataset

Dataset used: Food Recommendation System - Kaggle

Files:

food.csv: contains food metadata (ID, name, cuisine, course, diet)

ratings.csv: contains user ratings (userId, foodId, rating)

⚙️ Methodology

📌 1. Data Preparation

Clean and preprocess textual features: name, cuisine, course, diet

Combine into a single text column for vectorization

Transform text using TF-IDF Vectorizer

Convert rating matrix for collaborative filtering

📌 2. Content-Based Filtering

Compute similarity between foods using cosine similarity on TF-IDF vectors.

📌 3. Collaborative Filtering

Apply Truncated SVD to the user-item rating matrix to predict ratings for unseen items.

📌 4. Hybrid Filtering

Final recommendation score is computed by:

final_score = alpha * similarity_score + (1 - alpha) * predicted_rating

With alpha = 0.5 for balanced weighting.

📈 Evaluation

Evaluation metrics used:

Precision@5 = 0.25

Recall@5 = 0.25

These metrics show that 25% of top-5 recommended foods are relevant for a test user.

📌 Project Structure

food_recommendation/
│
├── food.csv
├── ratings.csv
├── food_recommendation.ipynb   ← Main notebook with documentation
├── laporan.md                   ← Final report (Bahasa Indonesia)
└── README.md                    ← This file

🧐 Tools & Libraries

Python 3

Pandas, NumPy

Scikit-learn

Matplotlib, Seaborn

NLTK (for text cleaning)

📚 References

Kaggle Dataset

Scikit-learn Documentation

NLTK for NLP

Recommendation System Guides - Google Developers

✍️ Author

Benny Alaster
