# Movies_Recommendation
Enter a Movie's name and based on the similarity,it will provide the best similar 5 movies 

Summary:
This project implements a Content-Based Movie Recommendation System using Python, Pandas, NLP and Cosine Similarity on the TMDB 5000 Movies dataset. The dataset was last updated on 2017

Project Pipeline and Methodology
1. Data Acquisition and Merging
Steps: Loaded the TMDB movies and credits datasets using kagglehub and merged them on the shared title column.
Why I did this: It combines descriptive attributes (genres, keywords, overview) with metadata (cast, crew) into a single dataset for rich content representation.
2. Feature Selection and Cleaning
Steps: Selected fllowing columns (movie_id, title, overview, genres, keywords, cast, crew), removed missing values, and dropped duplicates.
Why I did this: Reduces noise and ensures high-quality input data by focusing only on metadata that drives recommendation relevance.
3. Feature Parsing and Extraction

Steps: Processed nested JSON structures in genres, keywords, cast, and crew using abstract syntax trees (ast.literal_eval) to extract names (limiting cast to the top 3 actors and crew to the director).
Why I did this: Converts raw string representations of metadata into structured python lists. Else it was throwing the error for no value in list

5. Text Normalization and Space Collapsing
Steps: Stripped spaces from names using Porter Stemmer (e.g., "Sam Worthington" to "SamWorthington")
and merged all word lists (overview, genres, keywords, cast, crew) into a unified tags column.
Why I did this: Merging terms prevents the system from confusing unique entities (like directors and actors sharing a first name) and simplifies indexing.

7. Lowercasing and Stemming
Steps: Applied lowercasing and the NLTK PorterStemmer to stem the word tokens within the tag strings.
Why I did this: It standardizes vocabulary by collapsing grammatical variations of words (e.g., "loved" and "loving" to "love") to improve indexing matching.

9. Text Vectorization
Steps: Utilized CountVectorizer from scikit-learn to convert text tags into a matrix of bag-of-words token counts, limited to the top 5000 most frequent words.
Why I did this: Translates qualitative textual content into quantitative numerical vectors suitable for geometric similarity calculations.
10. Distance Measurement (Cosine Similarity)
    
Steps: Computed pairwise cosine similarity between all vectorized movie representations.
Why I did this: Calculates the directional similarity (angle) between high-dimensional vectors, evaluating how closely related two movies' thematic contexts are, independent of text length.
12. Recommendation Algorithm
Steps: Built a recommendation query function that looks up a movie's index, sorts its similarity scores in descending order, and displays the top 5 closest matches (excluding itself).
Why I did this: Allows the user to enter and get the similar movies name

Further Implimentations:
Build a UI(particularly Streamlit) tht will allow an interactive user based search engine and a profile such that their searches remain available to user whenever required.
