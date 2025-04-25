# DSA210 - Music Emotion Analysis Using Audio Features

## Project Overview
This project explores the relationship between audio features and the genres of music. By analyzing songs using extracted features such as **MFCCs, chroma, tempo, and harmonic relations**, the goal is to determine if musical characteristics correlate with specific genres.

## Data Sources and Collection
- **Public Domain Music:** Songs from open datasets with existing genre labels.  
- **Self-Composed Music:** Additional short compositions recorded to increase dataset diversity.  
- **Processing Method:** Audio files (WAV/MP3) will be analyzed using **Librosa** to extract relevant sound features. 

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

---

## Detailed Feature Extraction

Using **Librosa**, I plan to extract a variety of audio features, which may include (but are not limited to):

1. **Time-Domain Features:**
   - **Zero Crossing Rate (ZCR):** Measures how frequently the signal crosses the zero amplitude axis, often correlated with the “percussiveness” of a sound.

2. **Frequency-Domain / Spectral Features:**
   - **Spectral Centroid:** Indicates where most of the signal’s energy is concentrated (the “center of mass” of the spectrum).
   - **Spectral Rolloff:** The frequency below which a certain percentage (usually 85%) of the total spectral energy lies.
   - **Spectral Bandwidth:** Describes the spread of the spectrum around its centroid.
   - **Chroma Features:** Captures the intensity of each of the 12 distinct semitone pitches (C, C#, D, …, B) in the music.
   - **Tonnetz (Tonal Centroid):** Represents tonal relationships in a 6D space, useful for detecting harmonic changes.
   - **RMS Energy:** The root-mean-square value of the audio signal, related to perceived loudness.

3. **Mel-Frequency Cepstral Coefficients (MFCCs):**
   - A widely used feature set that captures the short-term power spectrum of the audio in a way that approximates human auditory perception.

4. **Tempo and Beat Tracking:**
   - **Tempo (BPM):** Estimated beats per minute from the audio.
   - **Onset Detection:** Identifies the start of musical notes/events.



5. **(Manually Annotated) Tonality (Minor/Major):**
   - I will determine whether a piece is primarily in a major or minor key by examining its overall harmonic and melodic context.

By combining these features I aim to capture a comprehensive musical fingerprint for each track. These features will then be used to correlate with (or predict) the genres assigned to the music.


## Hypothesis:
     -**Null Hypothesis:** Audio features do not have a correlation with the genre of music.
     -**Alternative Hypothesis:** Audio features do have a correlation with the genre of music.

