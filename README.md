# DSA210
# Music Emotion Analysis Using Audio Features

## Overview
This project explores the relationship between audio features and the emotions conveyed by music. By analyzing songs using features like MFCCs, chroma, and tempo, the goal is to determine if certain musical characteristics correlate with specific emotions (e.g., happy, sad).

## Motivation
I have a passion for both music and data science. This project allows me to merge these interests by applying data science techniques to understand how musical elements contribute to emotional perception.

## Data Sources and Collection
- **Data Source:** Public domain songs and manually curated song list with known emotional labels.
- **Collection Method:** Audio files (WAV/MP3) will be processed using Librosa to extract relevant features.

## Methodology
1. **Data Collection:** Gather a small dataset of songs.
2. **Feature Extraction:** Use Librosa to extract MFCCs, chroma features, and tempo.
3. **Data Organization:** Store extracted features in a pandas DataFrame.
4. **Exploratory Data Analysis:** Visualize features using matplotlib and seaborn.
5. **Model Building:** Train a logistic regression model using scikit-learn to classify emotions.
6. **Evaluation:** Analyze model performance and visualize results.

## How to Reproduce
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/DSA210_MusicEmotionAnalysis.git
