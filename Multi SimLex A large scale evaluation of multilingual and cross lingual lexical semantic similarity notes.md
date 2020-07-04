## Multi SimLex: A large scale evaluation of multilingual and cross lingual lexical semantic similarity

<https://multisimlex.com/>

### Problem

- Lack of annotated data for many tasks and domains hinders the development of computational models for the majority of the world’s languages.
- There is a need to guide and advance multilingual and cross-lingual NLP through annotation efforts that follow cross-lingually consistent guidelines.
- There are very few datasets for semantic similarity. Especially for low-resource languages such as Welsh, Kiswahili etc. Even if such datasets do exist they are constrained by their small size.
- Performing Cross-Lingual analysis with these datasets if also a challenge as there are created using different heterogenous construction procedures with different guidelines
- Consistent annotations and guidelines would advance research in multilingual parsing, cross-lingual parser transfer and enable a range of insightful studies on languages’ syntactic similarities and dissimilarities.

### Goals of this paper

- For these reasons the authors have made - Multi-SimLex. A suite of manually and consistently annotated semantic datasets for 12 different languages, focused on the fundamental lexical relation of semantic similarity (whether the pair of words share the same functional features).
- This paper also proposes a translation and annotation protocol for developing monolingual Multi-SimLex datasets with aligned concept pairs for typologically diverse languages. A consistent protocol leads to data with higher inter-annotator agreement.
- The proposed construction paradigm also supports the automatic creation of 66 cross-lingual Multi-SimLex datasets by interleaving the monolingual ones. The authors also give an outline of the construction of the cross-lingual datasets.
- They also benchmark a series of representational learning models on this new evaluation data.
- The experiments are used to answer various questions such as -  is it viable to extract high-quality word-level representations from pretrained encoders receiving sub word-level tokens as input? What are the implications of monolingual pretraining versus (massively) multilingual pretraining for performance? Can we effectively transfer available external lexical knowledge from resource-rich languages to resource lean languages to learn word representations?

### Creation of the Multi-SimLex resource

<u>Language Selection</u>

- The main objective for the inclusion criteria was to balance language prominence (by number of speakers of the language) for maximum impact of the resource, while simultaneously having a diverse suite of languages based on their typological features (such as morphological type and language family).
- There is a mixture of fusional, agglutinative, isolating, and introflexive languages that come from eight different language families.
- The various languages of this dataset are-
  - ARA (Arabic)
  - CMN (Mandarin Chinese)
  - CYM (Welsh)
  - ENG (English)
  - EST (Estonian)
  - FIN (Finnish)
  - FRA (French)
  - HEB (Hebrew)
  - POL (Polish)
  - RUS (Russian)
  - SPA (Spanish)
  - SWA (Kiswahili)
  - YUE (Yue Chinese)



<u>The work on data collection can be divided into two crucial phases -</u>

1.  A translation phase where the extended English language dataset with 1,888 pairs is translated into eleven target languages
2. An annotation phase where human raters scored each pair in both translated set and English set.



<u>Word Pair Translation</u>

Translators for each target language were instructed to find direct or approximate translations for the 1,888-word pairs that satisfy the following rules- 

1. All pairs in the translated set must be unique (i.e. no duplicate pairs)
2. Translating two words from the same English pair into the same word in the target language is not allowed (e.g. it is not allowed to translate car and automobile to the same Spanish word coche).
3. The translated pairs must preserve the semantic relations between the two words when possible. This means that, when multiple translations are possible, the translation that best conveys the semantic relation between the two words found in the original English pair is selected.
4. If it is not possible to use a single-word translation in the target language, then a multi-word expression (MWE) can be used to convey the nearest possible semantics given the above points (e.g., the English word homework is translated into the Polish MWE praca domowa).



The quality of the dataset was measured by asking human annotators to score how similar word pairs were and then the computing the average agreement for each annotator with other annotators using two metrics-

- Average Pairwise Inter-Annotator Agreement (APIAA)
- Average Mean Inter-Annotator Agreement (AMIAA)

The results indicated strong agreement with both metrics.

<u>Creation of Cross-lingual dataset</u>

- Given two languages we intersect their aligned concept pairs obtained through translation. The scores of cross-lingual pairs are then computed as averages of the two corresponding monolingual scores.
- In order to filter out concept pairs whose semantic meaning was not preserved during this operation,  we retain only cross-lingual pairs for which the corresponding monolingual scores differ at most by one  fifth of the full scale.



### Monolingual and Cross-Lingual Evaluation of Representation Learning Models

- The authors have benchmarked a series of representation learning models on this data and compare their performance.

<u>Models in comparison (monolingual)</u>

- Static Word Embeddings in Different Languages - 300 dimensional FASTTEXT word vectors trained of CC+Wiki text corpus.
- Unsupervised Post-Processing steps are applied post-training on pretrained input word embeddings. This is done to assess the usefulness of these processes. The processes applied are -
  1. Mean Centering (MC)
  2. All-but-the-top (ABBT)
  3. UNCOVEC
- Contextualized Word Embeddings

<u>Models in Comparison (cross-lingual)</u>

- Static Word Embeddings - VECMAP - 
  1.  The fully unsupervised variant - UNSUPER
  2.  The supervised variant SUPER
  3.  A supervised variant with self-learning SUPER + SL
- Contextualized Cross-Lingual Word Embeddings - Multilingual pretrained models, M-BERT and XLM-100.

<u>Results and Discussion</u>

- Unsupervised post-processing techniques (mean centering, elimination of top principal components, adjusting similarity orders) are always beneficial independently of the language, although the combination leading to the best scores is language-specific and hence needs to be tuned.
- Similarity rankings obtained from word embeddings for nouns are better aligned with human judgments than all the other part-of-speech classes considered here (verbs, adjectives, and, for the first time, adverbs). This confirms previous generalizations based on experiments on English.
- The factor having the greatest impact on the quality of word representations is the availability of raw texts to train them in the first place, rather than language properties (such as family, geographical area, typological features).
- Massively multilingual pretrained encoders such as M-BERT and XLM-100 fare quite poorly on our benchmark, whereas pretrained encoders dedicated to a single language are more competitive with static word embeddings such as fastText . Moreover, for language specific encoders, parameter reduction techniques reduce performance only marginally.
- Techniques to inject clean lexical semantic knowledge from external resources into distributional word representations were proven to be effective in emphasizing the relation of semantic similarity. In particular, methods capable of transferring such knowledge from resource-rich to resource-lean languages increased the correlation with human judgments for most languages, except for those with limited unlabeled data.
