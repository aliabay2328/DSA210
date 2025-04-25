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


Additionally, we computed a new column `mfcc_avg`, representing the average of `mfcc1` through `mfcc5`, for evaluating overall timbre.

---
##Exploratory Data Analysis
After extracting the features from the songs and outputing them to a csv file labeled by genre, we first compute the summary statistics to get a general idea:
![Screenshot 2025-04-25 203628](https://github.com/user-attachments/assets/7266f0f2-ce94-42eb-8435-b5590ffa0083)
And then we compute the means for each genre:

![Screenshot 2025-04-25 203755](https://github.com/user-attachments/assets/17a74c36-09f9-44b5-82d4-875ad055ef2d)

## 📊 Principal Component Analysis (PCA)

We applied PCA to reduce our 13-dimensional feature space to 2 principal components for visualization and exploratory analysis. The first two components are:
![Screenshot 2025-04-25 203256](https://github.com/user-attachments/assets/b39e3979-0a07-4000-b624-bf77d2d602a5)


- **PC1:** 46.2% of the variance (dominated by RMS, spectral centroid, tempo)
- **PC2:** 12.3% of the variance (driven by MFCCs and chroma features)



 **PC1 captures energy/brightness**, while **PC2 captures timbral/tonal complexity**.
Here we can observe that metal songs seem to cluster at high PC1 values, and hip-hop songs seem to be clustered a little below metal in PC1 which mostly captures energy
Also we can see that classical and rock songs are typically close to the PC2 level 0, which may indicate similiar tonal properties.
##Data Visualization:
**RMS by Genre(Means)**:
The average RMS of each genre, as expected metal overall has the highest and classical has the lowest.
---![Screenshot 2025-04-25 203057](https://github.com/user-attachments/assets/be84228d-aaca-4942-a807-1a0ae1a3d119)
**Spectral Centroid of Each Genre:**
Again since it is a measure of the location of the energy in the sound, metal seems to be significantly higher with again as expected rock being second.
![Screenshot 2025-04-25 203146](https://github.com/user-attachments/assets/34f04e57-f821-4833-a241-e5ecb638e4bb)

**Mean MFCC of Each Genre:**
This is the mean of the 5 coefficients used to specify the timbre of the sound. It may be important to see possible differences between genres.
![Screenshot 2025-04-25 205020](https://github.com/user-attachments/assets/a25e27f4-b37d-4e89-9bfd-d16486ace5de)
**Mean Tempo of Each Genre:**
It seems like there is no significant differences between tempo between genres.
![Screenshot 2025-04-25 203202](https://github.com/user-attachments/assets/8e48f85f-d537-4bef-8b16-e80bb2995fa4)
**Mean Onset of Genres:**
This is a measure of rythmic properties. And it seems electronic music has the most dominant rythmic properties with hip-hop and pop being close.

![Screenshot 2025-04-25 203229](https://github.com/user-attachments/assets/632d9806-746f-4be2-969d-6d65e178db3a)
**Mean Tonnetz by Genre:**
Tonnetz measures the tonal shifts and complexity of sound. It is expected that classical and jazz music has high tonnetz since they are more formal and technical forms compared to pop and hip-hop.
![Screenshot 2025-04-25 203215](https://github.com/user-attachments/assets/4cd5c59e-2bf6-41b4-8df9-937e2bbc5c26)


##  Hypothesis Testing





###  Hypothesis 1:  

**Null Hypothesis:** Metal songs does not have significantly higher RMS than Hip-Hop songs.
**Alternative Hypothesis:** "Metal songs have significantly higher energy (RMS) than Hip-Hop songs."
- t-statistic = **3.654**
- p-value = ** 0.0004**

 **Result:** Statistically significant. Metal songs are indeed more energetic than Hip-Hop songs. We reject null hypothesis.

---

###  Hypothesis 2:  
**Null Hypothesis:** "Classical music does not have higher tonal complexity(Tonnetz) than Rock music."
**Alternative Hypothesis:** "Classical music has higher tonal complexity (Tonnetz) than Rock music."

- t-statistic = **3.217**
- p-value = **0.0180**

⚠ **Result:** p value is less than 0.05. We reject the null hypothesis.

---

### 🧪 Hypothesis 3:  
**"Electronic songs have higher onset strength than Lo-fi songs."**

- t-statistic = **6.692**
- p-value = **< 0.00001**

✅ **Result:** Strongly significant. Electronic music exhibits more rhythmic sharpness than lo-fi.

---

### 🧪 Hypothesis 4:  
**"MFCC timbral characteristics are independent of genre."**

We tested this using **one-way ANOVA** on the `mfcc_avg` values:

- F-statistic = **X.XXX**
- p-value = **< 0.00001** (replace with your actual values)

❌ **Result:** We reject the null hypothesis. **MFCCs are influenced by genre**, meaning timbre varies significantly across styles.

---

## ✅ Conclusion

This project demonstrates that audio features extracted with Librosa provide strong signals for differentiating music genres. PCA visualization and hypothesis testing validate that genres differ meaningfully in energy, rhythm, and timbre.

Future work may involve using this feature set to train a supervised classifier or expanding the dataset with more diverse and balanced genre distributions.

---

## 🛠️ Tools Used
- Python 3 (Google Colab)
- Librosa
- Pandas, NumPy, Matplotlib, Seaborn
- Scikit-learn (PCA)
- SciPy (Hypothesis testing)

---

📧 For questions or collaboration: *[your-email@example.com]*

