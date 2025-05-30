# Music Genre Classification Using Audio Features

## Overview
This project investigates the relationship between musical genres and audio features extracted from songs. Using signal processing techniques with **Librosa** and applying statistical analysis and machine learning models, the goal is to examine whether different genres exhibit distinguishable patterns in features such as **MFCCs**, **chroma**, **tempo**, and **harmonic content**.

The project includes:
- Feature extraction using standard audio processing techniques,
- Exploratory data analysis (EDA) and principal component analysis (PCA),
- Hypothesis testing to validate feature differences between genres,
- Supervised learning models (Decision Tree, kNN with feature ablation, Logistic Regression) for classification tasks.

## Files
- `music_genre_classification.ipynb` — Main Jupyter notebook containing all code for feature analysis and model training.
- `requirements.txt` — Python package dependencies.
- `README.md` — Project description and setup instructions.
- `music_features.csv` - Extracted features in csv format.

## Data
The original feature extraction was performed on a dataset of approximately **500 songs**, which are not included here due to size. The extracted features are included. 



> **Important**: The project expects the feature CSV file to be uploaded to your **Google Drive** before running the notebook.

## Setup Instructions
All code used is included in the jupiter notebook, they expect to be run one after the other. To reproduce my analysis simply upload the feature csv to google drive and run the codes together(the code for feature extraction is used on the song dataset, therefore ıt does not need to be runned.)
DISCLAIMER-- Plotting the decision tree may yield unexpected results based on runtime. 
