# Problem of Interest

*  Models for predicting distributional word meaning representations from
brain imaging data

* Desired output of the model is a word embedding that could be useful in downstream tasks, possibly a brain2text encoder-decoder. 

* Obtaining decent accuracy for predicting distributional representations could facilitate the development of
a ‘mind reading’ device with numerous practical applications such as an aid for patients with dusfunctions.


# Experiments on Subjects (For data collection)

* Stimulus words presented to participants and their brain activity recorded
* Stimulus words presented in three different ways - the written word plus an image representing the word, the
word in a word cloud, and the word in a sentence

<b>Note</b> - Data for different participants cannot be directly combined due to differences in brain organization. Decoders are always
trained for each participant individually.


# Data


* Words for the experiments selected by clustering a pre-trained GloVe space consisting of 30,000 words into regions, and then
manually selecting a word from each region to yield a set of 180 content words that include nouns, verbs, and adjectives.

* Combined representation created for each word by averaging the fMRI images from the three stimulus presentation paradigms for each participant

* A vector space created for every participant whose dimensions are voxel activation values
in that participant’s brain scan. Feature selection carried out from this space to be used in the model.


# Method


* Ridge regression model trained for mapping the fMRI brain space to the GloVe space (Ridge regression is particularly useful when the number of parameters is comparable to the number of training samples.)

* Fully connected neural network by flattening features.

* CNNs


# Result Metrics


* <b>Pairwise Accuracy</b><br>
Calculated by considering all possible pairs of words (u, v) in the vocabulary and computing the similarity(Pearson correlation) between
the predictions (pu, pv) for these words and their corresponding target word embeddings (gu,gv). <br>
Accuracy is then defined as the fractionof pairs where ‘the highest correlation was between a decoded vector and the corresponding
text semantic vector’.

* <b>Rank Accuracy</b><br>
Calculated by computing thecorrelation, for every word in the vocabulary, between the predicted word embedding for that word
and all of the target word embeddings, and then ranking the target word embeddings accordingly.<br>
The accuracy score for that word is then defined as 1 − (rank − 1)/ ( |V| − 1 ), <br>
where rank is the rank of the correct target word embedding. This accuracy score is then averaged over
all words in the vocabulary

* <b>R2 Scores</b>

* <b>Cosine Similarity</b>


# Results 

* All models beat a simple baseline model that predicts vectors of random numbers (except
on the R2 metric, where the fully connected network performs below baseline)

* Performance on the Pair and Rank scores is generally good, but performance on the
other metrics is much worse

* Cos similarity is very low and R2 scores are negative, meaning that the predicted
word embeddings are very far in semantic space from where they should be


# Issues


* None of the tested models learns a good cross-space mapping: the predicted semantic vectors are far from their expected location and fail to capture the target space’s similarity structure. 

* Meanwhile, excellent performance is achieved on pairwise and rank-based classification
tasks, which implies that the predictions contain sufficient information for reconstructing stimulus
word labels


# Proposed Work


* Use data from experiments wherein subjects read not only individual words, but multiple words with context among those words (like sentences)

* Map these contextual brain embeddings to contextual language models like Word2Vec.

* Possibly explore better models than simple CNNs for mapping the fMRI images.




# References


* [Towards reconstructing intelligible speech from the human auditory cortex](https://www.nature.com/articles/s41598-018-37359-z)
* [From brain space to distributional space:the perilous journeys of fMRI decoding](https://www.aclweb.org/anthology/P19-2021.pdf)


