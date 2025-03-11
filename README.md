# DSA210 - Music Emotion Analysis Using Audio Features

## Project Overview
This project explores the relationship between audio features and the emotions conveyed by music. By analyzing songs using extracted features such as **MFCCs, chroma, tempo, and harmonic relations**, the goal is to determine if musical characteristics correlate with specific emotions like happiness, sadness, or tension.

## Data Sources and Collection
- **Public Domain Music:** Songs from open datasets with existing emotion labels.  
- **Self-Composed Music:** Additional short compositions recorded to increase dataset diversity.  
- **Processing Method:** Audio files (WAV/MP3) will be analyzed using **Librosa** to extract relevant sound features. Harmonic and tonal structures will also be examined manually when needed.

## Tools and Technologies
- **Python** (for data processing and analysis)  
- **Librosa** (feature extraction)  
- **Pandas** (data organization)  
- **Matplotlib & Seaborn** (visualization)  
- **Scikit-learn** (basic classification models)  

## Analysis Plan
1. **Feature Extraction:** Process raw audio files and extract musical properties.  
2. **Exploratory Data Analysis (EDA):** Identify trends and patterns in the extracted features.  
3. **Classification:** Train a model to predict emotional categories based on music features.  
4. **Evaluation:** Assess the model’s accuracy and interpret key results.  


