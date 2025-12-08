# CSC173 Deep Computer Vision Project Proposal
**Student:** [Joseph Jr Q. Corpuz], [2020-1360]  
**Date:** [12-12-2025]

## 1. Project Title 
[What makes a music popular: A comparative Association Rule Mining study on popular and unpopular music]

## 2. Problem Statement
[Spotify is a platform used for listening to music and collecting large amounts of data about songs, including which ones become popular. But what actually makes a song popular?
This project uses Association Rule Mining to identify combinations of song features that frequently appear in popular tracks versus unpopular ones. By uncovering these hidden patterns, the study aims to help emerging artists understand what characteristics may contribute to success, and to help listeners discover new music that matches their preferences.]

## 3. Objectives
- Convert features into categorical bins.
- Represent each track as a transaction of items.
- Apply FP-Growth to mine fequent itemset and generate association rules for popular and unpopular tracks.
- Compare rules using support, confidence, and lift to identify patterns that distinguish hits from less popular songs.
- Visualize key rules and interpret the musical and cultural significance of the findings.

## 4. Dataset Plan
- Source: [(https://www.kaggle.com/datasets/solomonameh/spotify-music-dataset/data?select=high_popularity_spotify_data.csv)]
- Classes: [Track popularity, Data Features (loudness, valence, danceablity, etc.), Playlist Genre, Track Name, Track Artist]
- Acquisition: [Manually download and extract it into the project directory on Windows]

## 5. Technical Approach
- Treat each song as a transaction containing categorical items derived from audio adn discriptive features. Use a transaction-based data mining pipeline to discover frequent patterns.
- Model: [Apply FP-Growth to identify frequent itemsets and generate association rules that link combinations of song attributes to popularity.]
- Framework: [mplement the pipeline in Python using pandas for data handling and mlxtend for FP-Growth and association rule mining.]
- Hardware: [CPU-only]

## 6. Expected Challenges & Mitigations
- Challenge: A lot of different genres and sub genres
- Solution: Dont show sub-genres and focus only on genres, allocate rare genres to "other"
- Challenge: Discretizing audio features leading to loss of information
- Solution: Define bins as thresholds for flexible interpretation