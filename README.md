# 🎬🍿 Movie Recommendation System

A content-based movie recommendation project built with Python. 
It suggests movies similar to a selected title using **cosine similarity** and a Streamlit app displays both the recommendations and their posters fetched from the TMDB **API**.

## Overview
Movies share similarities based on their genres, cast, crew, keywords, and descriptions.
This project analyzes these features, converts them into **vectors**, and **computes similarity scores** to recommend movies that are closest to a chosen title.

The System:
  - Processes movie metadata
  - Converts movie features into vectors
  - Measures how similar movies are with cosine similarity
  - Picks the most relevant matches for the selected title
  - Fetches posters using the TMDB API
  - Presents the recommendations through an user friendly Streamlit app

<img width="879" height="653" alt="image" src="https://github.com/user-attachments/assets/52f71399-7802-4a85-8dfd-9a882ac4cd55" />

## 💻 How it works

### 1. Data Loading
[Dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata)  
Two CSVs are used:
  - tmdb_5000_movies
  - tmdb_5000_credits
They’re merged on the movie title and trimmed to keep only what matters: genres, overview, keywords, cast, crew

### 2. Cleaning and preprocessing
  - genres, keywords, cast, and crew columns contain lists **encoded** as strings, so they’re converted into Python lists using ast.literal_eval.
  - Only the top three cast members are kept.
  - The director is extracted from the crew list.
  - Overviews are **tokenized** into word lists.
  - Spaces inside multi-word tokens (like Johnny Depp) are removed to avoid splitting them incorrectly.
  - All text features are merged into one giant tag list.

### 3. Stemming and vectorization
The tags are lowercased and **stemmed** with PorterStemmer.
Then **CountVectorizer** builds a **bag-of-words** representation with the top 5000 features and English stop words removed.

### 4. Similarity matrix
Cosine similarity is computed for all movie vectors.
This matrix powers the recommendation function.

### 5. Saving artifacts
Two pickles are stored in an artifacts folder:
  - movie_list.pkl (titles + tags)
  - similarity.pkl (**cosine similarity matrix**)
These files are loaded by the Streamlit app at runtime.

### 6. Streamlit application
The app takes a movie name, retrieves the closest matches based on similarity scores and fetches poster images from TMDB using the **API**.

## 🛠 How to Run the Project
### 1. Clone the Repository
```bash
git clone https://github.com/alpboraeris/movie-recommender-system.git
cd movie-recommender-system
```
### 2. Install Dependencies
```bash
pip install -r requirements.txt
```
### 3. Run the Streamlit App
```bash
streamlit run app.py
```

## 📐Future improvements
  - Mix in popularity or rating scores
  - Use embeddings from spaCy or sentence transformers
  - Add TF-IDF instead of CountVectorizer
