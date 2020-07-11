# Envisioned speech recognition using EEG sensors

## Original Publication

Kumar, P., Saini, R., Roy, P.P. et al. Envisioned speech recognition using EEG sensors. Pers Ubiquit Comput 22, 185–199 (2018). [https://doi.org/10.1007/s00779-017-1083-4](https://doi.org/10.1007/s00779-017-1083-4)

## Approach

This paper introduces a new robust 2 level coarse-to-fine classification approach. There are 3 main categories- digits, alphabets, and images. Each category has 10 classes in it. Therefore a total of 3x10 = 30 classes overall. So, a sample is first classified into one of these 3 categories and then into one of the sub-classes of that category. The paper also mentions text and non-text data wherein alphabet and digit come under text and images come under non-text data. 

## Experimental Setup

- 23 subjects from a dynamic age group of (15-40) years participated in this study.
- 14 electrode wireless bluetooth headset *Emotiv EPOC+* was used to capture the EEG signals.
- Initial sampling rate was 2048 Hz and was later downsampled to 128 Hz for each electrode.
- Each subject was shown 30 visual cues (Fig. 1) and was told to imagine the viewed object for 10 s while eyes closed in resting state.
- There was a gap of 20s between any 2 cues so that subject can return to the rest state before thinking of the next item.
- A total of 690 (23x30) recordings collected. Each recording was 10s in length.
- Each recording has been split into multiple signals for coarse and fine-level classification with different time duration of 250 ms and 50 ms, respectively. Therefore, a total of 138,000 (690x10s/0.05s) and 27,600 (690x10s/0.25s) recordings of EEG signals have been analyzed in this study at coarse and fine-level classification, respectively.

![Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled.png](Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled.png)

Fig. 1. The visual cues of all the 30 classes shown to subjects

## Preprocessing

### Signal Smoothing

Moving Average (MA) filter was used to remove the effect of unwanted electromyographic artifacts. It tends to smoothen the erratic peaks in a wave. 

![Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%201.png](Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%201.png)

Fig. 2. x[.], y' [.] show the input and output
signal

**M was chosen to be 5.** 

![Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%202.png](Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%202.png)

Fig. 3. Result of signal smoothing 

### Feature Extraction

From each smoothed signal, four different features, namely *Standard Deviation (SD), Root Mean Square (RMS), Sum of Values (SUM), and Energy (E)* were computed on all 14 electrodes. **Hence a new feature vector S(F) of 56 (14X4) dimensions was formed**.

                                                  S(F) = {SD,RMS, SUM,E}

## Methodology

- Random Forests were used for both the classification levels. A set of features were chosen randomly and a classifier was created with a bootstrapped sample of the training data.
- Each tree casts a unit vote for the most popular class to classify an input vector. Then, it combines the decision of a set of classifiers by weighted or unweighted voting to classify unknown examples. Thus, the majority voting technique is used to assign a class to the test sample.
- Gini index (GI) has been used as an attribute selection measure, which measures the impurity of an attribute with respect to the classes.

![Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%203.png](Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%203.png)

Fig. 4. Flowchart of the Classification Process

## Results

### Coarse-level classification

The results are computed using RF classifier by varying the number of trees in the forest. A maximum avg. accuracy of 85.20% was achieved with 32 trees. 

![Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%204.png](Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%204.png)

Fig. 5. Accuracy results at coarse-level 

### Finer-level classification

Here, the actual recognition of envision speech takes place. Recognition has been performed using three parallel RF classifiers by varying the number of trees in the forest from 1 to 50. Maximum accuracy of 68.46% has been recorded with the EEG signals recorded for imagined digits at 40 number of trees, whereas an accuracy of 66.91 and 65.72% has been recorded on characters and object images with 23 and 36 number of trees, respectively. 

Thus, an average recognition performance of 67.03% for all the three categories has been recorded.

![Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%205.png](Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%205.png)

Fig. 6. Accuracy results at fine-level

### Overall Accuracy

An overall accuracy of 57.11% was recorded when computed using RF classifier.

## Analysis

### Impact of aging on envisioned speech recognition

![Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%206.png](Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%206.png)

Table 1. Details of different age groups

![Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%207.png](Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%207.png)

Fig. 7. Accuracy results for different age groups

Lower recognition rates were recorded for the younger subjects belonging to G1 group. 

### Analysis of EEG duration for envision speech recognition

![Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%208.png](Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%208.png)

Fig. 8. Accuracy Results for different durations of EEG signals

Highest accuracy of 85.20% and 67.03% were recorded for coarse- and finer-level classification with durations of 250 and 50 ms, respectively. 

### Comparative Analysis of Modelling Algorithms

![Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%209.png](Envisioned%20speech%20recognition%20using%20EEG%20sensors%203c7c93798a114390893f9be7204319c2/Untitled%209.png)

Fig. 9. Accuracy Results for different classifiers

- Three classifiers were used in this research, Random Forests (RF), Support Vector Machines (SVM), Artificial Neural Networks (ANN).
- For ANN, a feed-forward neural network with two hidden and one output layer was implemented. Sigmoid function was used as activation function for all units. All weights have been initialized with small random values and a gradient-descent search in the networks weight space has been used for a minimum of squared error function of the networks output.
- Usually, ensemble methods result in more accurate solutions than a single model would and it was seen that the proposed RF classifier outperformed the other two classifiers.
