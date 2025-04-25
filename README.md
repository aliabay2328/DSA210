# DSA210 - Music Emotion Analysis Using Audio Features

## Project Overview
This project explores the relationship between audio features and the genres of music. By analyzing songs using extracted features such as **MFCCs, chroma, tempo, and harmonic relations**, the goal is to determine if musical characteristics correlate with specific genres.

## Data Sources and Collection
- **Public Domain Music:** Songs from open datasets with existing genre labels.  
- **Self-Composed Music:** Additional short compositions recorded to increase dataset diversity.  
- **Processing Method:** Audio files (WAV/MP3) were analyzed using **Librosa** to extract relevant sound features.

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

Using **Librosa**, a variety of audio features were extracted, including:

### Time-Domain Features:
- **Zero Crossing Rate (ZCR):** Measures how frequently the signal crosses the zero amplitude axis, often correlated with the “percussiveness” of a sound.

### Frequency-Domain / Spectral Features:
- **Spectral Centroid:** Indicates where most of the signal’s energy is concentrated (the “center of mass” of the spectrum).
- **Spectral Rolloff:** The frequency below which a certain percentage (usually 85%) of the total spectral energy lies.
- **Spectral Bandwidth:** Describes the spread of the spectrum around its centroid.
- **Chroma Features:** Capture the intensity of each of the 12 distinct semitone pitches (C, C#, D, ..., B) in the music.
- **Tonnetz (Tonal Centroid):** Represents tonal relationships in a 6D space, useful for detecting harmonic changes.
- **RMS Energy:** The root-mean-square value of the audio signal, related to perceived loudness.

### Mel-Frequency Cepstral Coefficients (MFCCs):
- A widely used feature set that captures the short-term power spectrum of the audio in a way that approximates human auditory perception.

### Tempo and Beat Tracking:
- **Tempo (BPM):** Estimated beats per minute from the audio.
- **Onset Detection:** Identifies the start of musical notes/events.

### Manually Annotated Tonality (Minor/Major):
- Determined whether a piece is primarily in a major or minor key by examining its overall harmonic and melodic context.

Additionally, a new column `mfcc_avg` was computed, representing the average of `mfcc1` through `mfcc5`, for evaluating overall timbre.

---

## Exploratory Data Analysis

After extracting the features from the songs and outputting them to a CSV file labeled by genre, we first computed the summary statistics to get a general idea:

![Screenshot 2025-04-25 203628](https://github.com/user-attachments/assets/7266f0f2-ce94-42eb-8435-b5590ffa0083)

Then, we computed the means for each genre:

![Screenshot 2025-04-25 203755](https://github.com/user-attachments/assets/17a74c36-09f9-44b5-82d4-875ad055ef2d)

---

## Principal Component Analysis (PCA)

We applied PCA to reduce our 13-dimensional feature space to 2 principal components for visualization and exploratory analysis. The first two components are:

![Screenshot 2025-04-25 203256](https://github.com/user-attachments/assets/b39e3979-0a07-4000-b624-bf77d2d602a5)

- **PC1:** 46.2% of the variance (dominated by RMS, spectral centroid, tempo)
- **PC2:** 12.3% of the variance (driven by MFCCs and chroma features)

**PC1 captures energy/brightness**, while **PC2 captures timbral/tonal complexity**.

Observations:
- Metal songs seem to cluster at high PC1 values, and hip-hop songs cluster slightly below metal on PC1, which mostly captures energy.
- Classical and rock songs are typically close to the PC2 level 0, which may indicate similar tonal properties.

---

## Data Visualization

**RMS by Genre (Means):**  
The average RMS of each genre; as expected, metal overall has the highest and classical has the lowest.
Also it can be observed that electronic music seems to have a high variance in energy.

![Screenshot 2025-04-25 203057](https://github.com/user-attachments/assets/be84228d-aaca-4942-a807-1a0ae1a3d119)

**Spectral Centroid by Genre:**  
Since it measures the center of energy in the sound, metal seems significantly higher, with rock being second.

![Screenshot 2025-04-25 203146](https://github.com/user-attachments/assets/34f04e57-f821-4833-a241-e5ecb638e4bb)

**Mean MFCC of Each Genre:**  
The mean of the 5 MFCC coefficients, specifying the timbre of the sound.


![Screenshot 2025-04-25 205020](https://github.com/user-attachments/assets/a25e27f4-b37d-4e89-9bfd-d16486ace5de)

**Mean Tempo by Genre:**  
There seem to be no significant differences in tempo between genres.

![Screenshot 2025-04-25 203202](https://github.com/user-attachments/assets/8e48f85f-d537-4bef-8b16-e80bb2995fa4)

**Mean Onset Strength by Genre:**  
A measure of rhythmic properties. Electronic music has the most dominant rhythmic properties, with hip-hop and pop close behind.
Also classical seems to be very significantly lower, which is again expected.

![Screenshot 2025-04-25 203229](https://github.com/user-attachments/assets/632d9806-746f-4be2-969d-6d65e178db3a)

**Mean Tonnetz by Genre:**  
Tonnetz measures tonal shifts and complexity. As expected, classical and jazz music show high Tonnetz values.

![Screenshot 2025-04-25 203215](https://github.com/user-attachments/assets/4cd5c59e-2bf6-41b4-8df9-937e2bbc5c26)

---

## Hypothesis Testing

### Hypothesis 1:
**Null Hypothesis:** Metal songs do not have significantly higher RMS than Hip-Hop songs.  
**Alternative Hypothesis:** Metal songs have significantly higher energy (RMS) than Hip-Hop songs.

- t-statistic = **3.654**
- p-value = **0.0004**

**Result:** Statistically significant. Metal songs are indeed more energetic than Hip-Hop songs. We reject the null hypothesis.

---

### Hypothesis 2:
**Null Hypothesis:** Classical music does not have higher tonal complexity (Tonnetz) than Rock music.  
**Alternative Hypothesis:** Classical music has higher tonal complexity (Tonnetz) than Rock music.

- t-statistic = **3.217**
- p-value = **0.0180**

**Result:** p-value is less than 0.05. We reject the null hypothesis.

---

### Hypothesis 3:
**Null Hypothesis:** Electronic songs do not have a higher onset strength than Hip-Hop songs.  
**Alternative Hypothesis:** Electronic songs have higher onset strength than Hip-Hop songs.

- t-statistic = **2.291**
- p-value = **< 0.03**

**Result:** Statistically significant. Electronic music exhibits more rhythmic sharpness than Hip-Hop. We reject the null hypothesis.

---

### Hypothesis 4:
**Null Hypothesis:** MFCC timbral characteristics are independent of genre.  
**Alternative Hypothesis:** MFCC timbral characteristics are not independent of genre.

We tested this using **one-way ANOVA** on the `mfcc_avg` values:

- F-statistic = **42.206**
- p-value = **< 0.00000000000000000000000000000000000000001**

**Result:** We reject the null hypothesis. MFCCs are influenced by genre, meaning timbre varies significantly across styles.

---

## Conclusion

This project demonstrates that audio features extracted with Librosa provide strong signals for differentiating music genres. PCA visualization and hypothesis testing validate that genres differ meaningfully in energy, rhythm, and timbre.

Future work may involve using this feature set to train a supervised classifier or expanding the dataset with more diverse and balanced genre distributions.

---

## Tools Used
- Python
- Librosa
- Pandas, NumPy, Matplotlib, Seaborn
- Scikit-learn (PCA)
- SciPy (Hypothesis testing)
