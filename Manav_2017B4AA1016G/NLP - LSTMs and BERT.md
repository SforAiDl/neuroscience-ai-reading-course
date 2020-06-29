# Assessing the Ability of LSTMs to Learn Syntax-Sensitive Dependencies

## Tasks

**Strongest supervision** - Number Prediction Task i.e. guessing the number of a verb based on the words that preceded it 

**Limited Supervision** - Provide the model with full sentences annotated as to whether or not they violate subject-verb number agreement

**No Supervision** -  Language Modelling i.e. Predicting the next word

![image-20200629115323143](Images\image-20200629115323143.png)



##### We Treat Subject-Verb Agreement as Evidence for Syntactic Structure

The potential presence of agreement attractor entails that the model must identify the head of the syntactic subject that corresponds to a given verb in order to choose the correct inflected form of that verb.(Intervening nouns with the opposite number from the subject are called agreement attractors)

### Number Prediction

In this task, the model sees the sentence up to but not including a present-tense verb. It then needs to guess the number of the following verb (a binary choice, either PLURAL or SINGULAR).

For example, The keys to the cabinet __________________                  (PLURAL)

In order to perform well on this task, the model needs to encode the concepts of **syntactic number** and **syntactic subjecthood** : it needs to learn that some words are singular and others are plural, and to be
able to identify the correct subject.

Overall Error - 0.83%

Noun Only Error - 4.2% (Common Nouns) , 4.5%(All Nouns)

This implies that around 95% of agreement dependencies can be captured based solely on the sequence of nouns preceding the verb

This suggests that function words, verbs and other syntactically informative elements play an important role in the model’s ability to correctly predict the verb’s number.

<img src="Images\image-20200629124208200.png" alt="image-20200629124208200" style="zoom:200%;" />

**Distance** - Performance did not degrade considerably when the distance between the subject and the verb grew up to 15 words (LSTMs - LONG, 3 gates)

**Relative Clauses** - Relative clauses with attractors are likely to be fairly challenging,

PP: The toy(s) of the boy(s)...                    (Prepositional Phase)

RC: The toy(s) that the boy(s)...                (Relative Clause)      

PP sentences the correct number of the upcoming verb is determined by the main clause subject toy(s);
in RC sentences it is determined by the embedded subject boy(s).

## Language Modelling

Predicting the next word i.e. instead of predicting SINGULAR or PLURAL for the following sentence, the word predicted should be 'are' and not 'PLURAL'

The keys to the cabinet __________________                         (are)

The LM model made too many errors as compared to the other Number Prediction models and in difficult cases, even performed worse than random guesses.

We conclude that LSTMs can learn to approximate structure-sensitive dependencies fairly well given explicit
supervision, but more expressive architectures may be necessary to eliminate errors altogether.

### Results

Number prediction model indeed managed to capture a decent amount of syntactic knowledge, but was overly reliant on function words.

 Error rates increased only mildly when we switched to more indirect supervision consisting only of sentence-level grammaticality annotations without an indication of the crucial verb.

By contrast, the language model trained without explicit grammatical supervision performed worse than chance on the harder agreement prediction cases.



# Assessing BERT’s Syntactic Abilities

### Tasks

Feed each sentence word by word, stop right before the focus verb, and ask the model to predict a binary plural/singular decision (supervised setup) or compare the probability assigned by a pre-trained language model (LM) to the plural vs singular forms of the verb (LM setup)

Replace each content word with random words from the same part-of speech and inflection This results in “coloreless green ideas” nonce sentences.

Construct minimal pairs of grammatical and ungrammatical sentences, feed each one in its entirety into a model, and compare the perplexity assigned by the model to the grammatical and ungrammatical sentences. The model is “correct” if it assigns the grammatical sentence a higher probability than to the ungrammatical one.

### BERT 

As the name suggests, BERT model is bi-directional and hence to adapt to the unidirectional setup of LSTMs, some changes need to be made.

I adapt the unidirectional setup by feeding into BERT the complete sentence, while masking out the single focus verb. I then ask BERT for its word predictions for the masked position,

(The results are not directly comparable to previous work: the BERT models are trained on different (and larger) data, are allowed to access the suffix of the sentence in addition to its prefix, and are evaluated on somewhat different data due to discarding OOV items)

I experiment with the bert-large-uncased and bert-base-uncased models. 

All cases exhibit high scores—in the vast majority of the cases substantially higher than reported in previous work.  The high performance numbers indicate that the purely attention-based BERT models are likely capable of capturing the same kind of syntactic regularities that LSTM-based models are capable of capturing, at least as well as the LSTM models and probably better.

<img src="Images\image-20200629114933142.png" alt="image-20200629114933142" style="zoom: 250%;" />

Another noticeable and interesting trend is that larger is not necessarily better: the BERT-Base model outperforms the BERT-Large model on many of the syntactic conditions.



# What does BERT learn about the structure of language?

Because the results(GLUE Benchmarks) are so good, we conclude that maybe BERT can learn the structural information about a language.

**Task**  - We perform a series of experiments to probe the nature of the representations learned by different layers of BERT.

For a token sequence, we compute the span representation at layer by concatenating the first and last hidden vector, along with their element-wise product and difference. We visualize the span representations
obtained from multiple layers using t-SNE.

![image-20200629123758820](Images\image-20200629123758820.png)

We observe that BERT mostly captures phrase-level information in the lower layers and that this information gets gradually diluted in higher layers.

(We further quantify this claim by performing a k-means clustering on span representations with k = 10, i.e. the number of distinct chunk types. Evaluating the resulting clusters using the Normalized Mutual Information (NMI) metric shows again that the lower layers encode phrasal information better than higher layers)

### Probing Tasks

We evaluate each layer of BERT using ten probing sentence-level datasets/tasks.

1. SentLen: Length of sentence

2. WC: Word occurrence detection

3. Treedepth: What is the depth of dependency tree

4. TopConst: Sequence of top level constituents in the syntax tree

5. BShift: Word Order detection

6. Tense: Tense of the sentence

7. SubjNum: Subject number in the main clause

8. ObjNum: Object number in the main clause

9. SOMO: Sensitivity to random replacement of noun/verb

10. CoordInv: Sensitivity to random swapping of coordinated clausal conjuncts

    

<img src="Images\image-20200629122407035.png" alt="image-20200629122407035" style="zoom:200%;" />

(Untrained - Random Weights)

We find that the untrained version of BERT corresponding to the higher layers outperforms the trained version in the task of predicting sentence length (SentLen).

This could indicate that untrained models contain sufficient information to predict a basic surface
feature such as sentence length, whereas training the model results in the model storing more complex
information, at the expense of its ability to predict such basic surface features.

### Subject-verb agreement

BERT learns syntactic phenomenon surprisingly well using various stimuli for subject-verb agreement.

<img src="Images\image-20200629123053250.png" alt="image-20200629123053250" style="zoom: 67%;" />

### Conclusions

Syntactic features were shown to be captured well in the middle layers.

BERT requires deeper layers to model long-range dependency information
