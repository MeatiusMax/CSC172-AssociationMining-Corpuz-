# [Project Title: What makes a music popular: A comparative Association Rule Mining study on popular and unpopular music]
**CSC173 Intelligent Systems Final Project**  
*Mindanao State University - Iligan Institute of Technology*  
**Student:** [Joseph Jr. Q. Corpuz], [2020-1360]  
**Semester:** [e.g., AY 2025-2026 Sem 1]  
[![Python](https://img.shields.io/badge/Python-3.8+-blue)](https://python.org) [![PyTorch](https://img.shields.io/badge/PyTorch-2.0-orange)](https://pytorch.org)

## Abstract
[Everyday there are over 120000 songs released, only a small percentage become popular. People have different tastes when it comes to music, some like hard music while others like chill beats. So that begs the question, what makes songs popular?. This project applies ARM (Association Rule Mining) to spotify dataset to identify feature combinations that correlates with the songs popularity. Combining popular and unpopular dataset of song features with both audio features and descriptive features. We preprocessed the data by discretizing the features into interpretable bins making it usable, then apply FP-GROWTH and mined association rules separately for both popular and unpopular song to discover frequent itemsets. The rules-set resulting from the ARM reveals interpretable patterns such as popular song having r&b genre whilst unpopular songs associates with low energy. The result also show that unpopular song exhibit consistent features while popular songs show greater diversity. These findings can be used in creative decision, especially in music production.][web:25][web:41]

## Table of Contents
- [Introduction](#introduction)
- [Related Work](#related-work)
- [Methodology](#methodology)
- [Experiments & Results](#experiments--results)
- [Discussion](#discussion)
- [Ethical Considerations](#ethical-considerations)
- [Conclusion](#conclusion)
- [Installation](#installation)
- [References](#references)

## Introduction
### Problem Statement
[Music streaming platforms like spotify shape how millions of users discover and listen to music. With over 120000 music uploaded every single day, only some ever make to popular mainstream music. The vast mahority of small music artists from all around the world often struggle to make it to the top. But it begs the question, What does these mainstream, popular music have that makes them popular?. This project addresses this gap by applying ARM to uncover hidden, data-driven patterns in spotify features and metadata that occurs with popularity. By identifying such patters, this aims to provide insights that can help artists make creative decisions and improve their chances at making it to the mainstream music.]

### Objectives
- [Objective 1: Convert Spotify features into usable and meaningful categorical bins]
- [Objective 2: Represent each track as a transaction of items for ARM]
- [Objective 3: Apply FP-Growth to mine frequent itemsets from both popular and unpopular songs]
- [Objective 4: Generate and compare association rules using support,confidence and lift]
- [Objective 5: Interpret rules to understand features that define popularity]

## Related Work
- [Paper 1: Dominic, D. D., Azween, B. & Abdullah, A. (2009). A Comparative Study of FP-growth Variations. undefined.][web:25]
- [Paper 2: Sidhu, S., Meena, U. K., Nawani, A., Gupta, H. & Thakur, N. (2014). FP Growth Algorithm Implementation. undefined, 93(8). ]
- [Gap: Determining features that correlates with popularity using Spotify dataset.] [web:25]

## Methodology
### Dataset
- Source: [(https://www.kaggle.com/datasets/solomonameh/spotify-music-dataset/data?select=high_popularity_spotify_data.csv)]
- Preprocessing: remove duplicates and missing values, Discretized numerical features into categorical bins, encde each track as a transaction of items.[web:41]

### Architecture
![ARM pipeline]
- Algorithm: FP Growth
- Min Support: 0.05
-Categorical Bin Example
|  Feature | Bin | Category|
| :--- | :---: | ---: |
| Energy | 0,0.3,0.7,1.0 | Low, Medium, High |

### Code Snippet
combined_df['energy_discretize'] = descretize_features(combined_df['energy'], bins=[0, 0.3, 0.7, 1], labels=['low_energy', 'medium_energy', 'high_energy'])
*********************
transactions = []
for _, row in arm_df.iterrows():
    transaction = [f"{col}={row[col]}" for col in arm_df.columns]
    transactions.append(transaction)
*********************
te = TransactionEncoder()
te_ary = te.fit(transactions).transform(transactions)
df = pd.DataFrame(te_ary, columns=te.columns_)
print("Encoded transactions into a DataFrame.")
print(df.head())


frequent_itemsets = fpgrowth(df, min_support=0.01, use_colnames=True)
print("Generated frequent itemsets.")
print(frequent_itemsets)

## Results
|Song Type|Features|Lift|Confidence|Support
Unpopular| valence_discretize=low_valence, danceability_discretize=medium_danceability, instrumentalness_discretize=high_instrumentalness, energy_discretize=low_energy, mode_discretize=major|1.54|1.0|0.014
Popular|speechiness_discretize=low_speechiness, loudness_discretize=high_loudness, energy_discretize=medium_energy, danceability_discretize=high_danceability, tempo_discretize=medium_tempo, liveness_discretize=low_liveness, instrumentalness_discretize=low_instrumentalness, duration_ms_descretize=long_duration|2.09|0.729|0.011

-[The FP-growth Algorithm identified frequent association rules for ppoular song. The strongles rule being if the song has low speechiness, high loudness,  medium energy, high danceability, medium tempo, low liveness, low instrumentalness, and long duration then it is bound to be popular. Having Support of 0.011, Confidence of 0.729, and Lift of 2.09.][web:25]
-[The upoular song show highly consistent featur combinations. The top results having low valence, medium danceability, high instrumentalness, low energy,and major mode tend to be unpopular. Having Support of 0.014, Confidence of 1.000, and Lift of 1.54][web:25]

### Demo
![Detection Demo](demo/detection.gif)
[Video: [CSC173_YourLastName_Final.mp4](demo/CSC173_YourLastName_Final.mp4)] [web:41]

## Discussion
[The result highlights a clear distinction between the popular and unpopular songs in terms of both features and association strength.][web:25]
[Popular songs are associated with medium tempo, high danceability and medium energy. The low instrumentalness and low speechiness suggest that popular tracks have little vocal and instrumentals but have energetic rythm and tempo that can be choreographed into a dance.][web:25]
[In contrast, unpopular songs exhibit highly uniform and repetitive feature combinations. The repeated occurrence of low energy, low valence, and high instrumentalness indicates that these tracks tend to be less rhythmically engaging with high usage of instruments and little words spoken. These unpopular rules suggests that whenever these specific feature combinations occur, the songs are always labeled as unpopular within the dataset. However, their lower lift values compared to popular rules indicate that these features are less distinctive and more common across the dataset.][web:25]
[The difference in confidence levels between popular and unpopular rules is notable. Popular rules show confidence values below 1.0, reflecting greater variability and diversity among popular songs, whereas unpopular songs are associated with more rigid and predictable patterns. This supports the idea that popularity is not driven by a single fixed audio formula, while unpopularity is often associated with constrained musical characteristics.][web:25]
[Overall these findings show the effectiveness of ARM in providing interpretable insights into music popularity using music features to see what specific features determine popularity.][web:25]


## Ethical Considerations
[This study uses publicly available data and does not involve personal or sensitive user information. However, care must be taken when applying such insights, as over-reliance on data-driven patterns may encourage formulaic creativity or bias against unconventional music styles.][web:41]

## Conclusion
[This project demonstrates the effectiveness of ARM in determining patterns related to music popularity. By comparing both popular and unpopular song, we get the differences in feature consistency and diversity.

Future work:
- Incoporate features such as dates and trends
- Use data from other platform aside from spotify 
- Mine rules per genre
]

## Installation
Clone repo: git clone https://github.com/MeatiusMax/CSC172-AssociationMining-Corpuz-
Install deps: pip install -r requirements.txt
Then run the code

**requirements.txt:**
asttokens==3.0.1
colorama==0.4.6
comm==0.2.3
contourpy==1.3.3
cycler==0.12.1
debugpy==1.8.19
decorator==5.2.1
executing==2.2.1
fonttools==4.61.1
ipykernel==7.1.0
ipython==9.8.0
ipython_pygments_lexers==1.1.1
jedi==0.19.2
joblib==1.5.3
jupyter_client==8.7.0
jupyter_core==5.9.1
kiwisolver==1.4.9
matplotlib==3.10.8
matplotlib-inline==0.2.1
mlxtend==0.24.0
nest-asyncio==1.6.0
numpy==2.3.5
packaging==25.0
pandas==2.3.3
parso==0.8.5
pillow==12.0.0
platformdirs==4.5.1
prompt_toolkit==3.0.52
psutil==7.1.3
pure_eval==0.2.3
Pygments==2.19.2
pyparsing==3.2.5
python-dateutil==2.9.0.post0
pytz==2025.2
pyzmq==27.1.0
scikit-learn==1.8.0
scipy==1.16.3
seaborn==0.13.2
six==1.17.0
stack-data==0.6.3
threadpoolctl==3.6.0
tornado==6.5.4
traitlets==5.14.3
tzdata==2025.3
wcwidth==0.2.14


## References

Sidhu, S., Meena, U. K., Nawani, A., Gupta, H. & Thakur, N. (2014). FP Growth Algorithm Implementation. undefined, 93(8). 

Dominic, D. D., Azween, B. & Abdullah, A. (2009). A Comparative Study of FP-growth Variations. undefined.


## GitHub Pages
View this project site: https://github.com/MeatiusMax/CSC172-AssociationMining-Corpuz- [web:32]