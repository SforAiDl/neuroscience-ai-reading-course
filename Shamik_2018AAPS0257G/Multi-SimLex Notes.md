Multi-SimLex notes

Paper - https://arxiv.org/abs/2003.04866

**1 Intro**

- Lack of annotated data for many tasks and domains hinders the development of computational models for the majority of the world&#39;s languages.
- There is a need to guide and advance multilingual and cross-lingual NLP through annotation efforts that follow cross-lingually consistent guidelines.
- Consistent annotations and guidelines advance research in multilingual parsing, cross-lingual parser transfer and enable a range of insightful studies on languages&#39; syntactic similarities and dissimilarities.
- Multi-SimLex is a suite of manually and consistently annotated semantic datasetsfor 12 different languages, focused on the fundamental lexical relation of semantic similarity(whether the pair of words share the same functional features). It is a lexical semantic similarity dataset.
- Discerning between semantic similarity and relatedness/association is crucial for theoretical studies on lexical semantics and has been shown to benefit a range of language understanding tasks in NLP such dialog state tracking, spoken language understanding, text simplification, dictionary and thesaurus construction.
- This paper also proposes a translation and annotation protocol for developing monolingual Multi-SimLex datasets with aligned concept pairs for typologically diverse languages.
- This dataset creation protocol yields data with higher inter-annotator agreement.
- unified construction protocol and alignment between concept pairs enables a series of quantitative analyses.
- Data created according to Multi-SimLex protocol also allow for probing into whether similarity judgments are universal across languages, or rather depend on linguistic affinity (in terms of linguistic features, phylogeny, and geographical location, section 5).
- Multi-SimLex datasets can be used as an intrinsic evaluation benchmark to assess the quality of lexical representations based on monolingual, joint multilingual, and transfer learning paradigms (section 7).
- The proposed construction paradigm also supports the automatic creation of 66 cross-lingual Multi-SimLex datasets by interleaving the monolingual ones. (section 6)
- There is an outline of the construction of the cross-lingual datasets in section 6.
- Quantitative evaluation of a series of cutting-edge cross-lingual representation models on this benchmark are in section 8.

**2 Lexical Semantic Similarity**

**2.1 Similarity and Association**

- The focus of the Multi-SimLex initiative is on the lexical relation of pure semantic similarity.
- For any pair of words, this relation measures whether their referents share the same features.
- This relation semantic similarity can be contrasted with cognitive association, which often depends on how much their referents interact in the real world, or are found in the same situations.
- Semantic similarity and association overlap to some degree, but do not coincide.
- There exist plenty of pairs that are intuitively associated but not similar. Pairs where the converse is true can also exist but are rarer.
- A key property of semantic similarity is its gradience: pairs of words can be similar to a different degree. On the other hand, the relation of synonymy is binary: pairs of words are synonyms if they can be substituted in all contexts (or most contexts, in a looser sense), otherwise they are not.
- While synonyms can be conceived as lying on one extreme of the semantic similarity continuum, it is crucial to note that their definition is stated in purely relational terms, rather than invoking their referential properties.
- This makes behavioural studies on semantic similarity fundamentally different from lexical resources like WordNet, which include paradigmatic relations (such as synonymy).

**2.2**  **Similarity for NLP: Intrinsic Evaluation and Semantic Specialization**

- Distributional methods obscure a crucial facet of lexical meaning.
- This limitation also reflects onto word embeddings (WEs), representations of words as low-dimensional vectors that have become indispensable for a wide range of NLP applications.
- In particular, it involves both static WEs learned from co-occurrence patterns and contextualized WEs learned from modelling word sequences.
- As a result, in the induced representations, geometrical closeness (measured e.g. through cosine distance) conflates genuine similarity with broad relatedness.
- WEs learned from texts annotated with syntactic information mirror similarity better than simple local bag-of-words neighbourhoods.
- The failure of WEs to capture semantic similarity, in turn, affects model performance in several NLP applications where such knowledge is crucial.
- In particular, Natural Language Understanding tasks such as statistical dialog modelling, text simplification, or semantic text similarity suffer the most.
- As a consequence, resources providing clean information on semantic similarity are key in mitigating the side effects of the distributional signal.
- In particular, such databases can be employed for the intrinsic evaluations of specific WE models as a proxy of their reliability for downstream applications.
- The more WEs are misaligned with human judgments of similarity, the more their performance on actual tasks is expected to be degraded.

  Similarity and Language Variation: Semantic Technology

- In this work, the concept of (true) semantic similarity is tackled from a multilingual perspective.
- While the same meaning representations may be shared by all human speakers at a deep cognitive level, there is no one-to-one mapping between the words in the lexicons of different languages. This makes the comparison of similarity judgments across languages difficult, since the meaning overlap of translationally equivalent words is sometimes far less than exact.
- This results from the fact that the way languages &#39;partition&#39; semantic fields is partially arbitrary, although constrained cross lingually by common cognitive biases.
- For instance, consider the field of colours: English distinguishes between green and blue, whereas Murle (South Sudan) has a single word for both.
- Semantic Typology studies the variation in lexical semantics across languages.
- According to (Evans 2011), the ways languages categorize concepts into the lexicon follow three main axes:

1) Granularity: what is the number of categories in a specific domain?

2) Boundary location: where do the lines marking different categories lie?

3) Grouping and dissection: what are the membership criteria of a category; which instances are considered to be more prototypical?

- Different choices w.r.t these axes lead to different lexicalization patterns.

**3. Previous Work and Eval Data**

Word Pair Datasets:

- Rich expert-created resources such as WordNet, VerbNet, or FrameNet encode a wealth of semantic and syntactic information, but are expensiveand time-consuming to create.
- The scale of this problem gets multiplied by the numberof languages in consideration.
- Therefore, crowd-sourcing with non-expert annotatorshas been adopted as a quicker alternative to produce smaller and more focused semantic resource and evaluation benchmarks.
- This alternative practice has had a profound impact on distributional semantics and representation learning.
- While some prominent English word pair datasets such as WordSim-353, MEN, or Stanford Rare Words did not discriminate between similarity and relatedness, the importance of this distinction was established through the creation of SimLex-999.
- This inspired other similar datasets which focused on different lexical properties. For instance, SimVerb-3500 provided similarity ratings for 3,500 English verbs, whereas CARD-660 aimed at measuring the semantic similarity of infrequent concepts.

Semantic Similarity Datasets in Other Languages:

- The dominant approach to create similar resources is translating and reannotating the entire original English SimLex-999 dataset, as done previously for German, Italian etc.
- Semantic differences among languages can have a profound impact on the annotation scores.
- These differences even roughly define language clusters based on language affinity.
- A core issue is the lack of one unified procedure that ensures the comparability of resources in different languages.
- Another issue is, concept pairs for different languages are sourced from different corpora (e.g., direct translation of the English data versus sampling from scratch in the target language).
- The previous SimLex-based multilingual datasets inherit the main deficiencies of the English original version, such as the focus on nouns and highly frequent concepts.
- Prior work mostly focused on languages that are widely spoken and do not account for the variety of the world&#39;s languages.
- One of the goals of this paper is to devise a standard methodology to extend the coverage to multiple languages even ones that are resource-lean and/or typologically diverse (e.g. Welsh, Kiswahili etc).

Multilingual Datasets for Natural Language Understanding:

- The Multi-SimLex initiative and corresponding datasets are also aligned with the recent efforts on procuring multilingual benchmarks that can help advance computational modelling of natural language understanding across different languages.
- BERT and XLM are typically probed on XNLI test data for cross-lingual natural language inference.
- XNLI was created by translating examples from the English MultiNLI dataset, and projecting its sentence labels.
- Other recent multilingual datasets target the task of question answering based on reading comprehension:

  1. MLQA – 7 languages, translated from an English dataset
  2. XQuAD – 10 languages, translated from an English dataset
  3. TyDiQA – 9 languages, built independently in each language

- PAWS-X – focused on paraphrase identification task and was created translating the original English PAWS into 6 languages.
- Multi-SimLex can substantially contribute to this endeavour by offering a comprehensive multilingual benchmark for the fundamental lexical level relation of semantic similarity.
- In future work, Multi-SimLex also offers an opportunity to investigate the correlations between word-level semantic similarity and performance in downstream tasks such as QA and NLI across different languages.

 **4 Base for Multi-SimLex: English SimLex-999**

- The design principle for ENG SimLex is the basis for all the Multi-SimLex datasets in other languages.
- Construction Criteria. The following criteria have to be satisfied by any high-quality semantic evaluation resource, as argued by previous studies focused on the creation of 
  such resources
  
     C1) Representative and diverse. The resource must cover the full range of diverse concepts occurring in natural language, including different word classes (e.g., nouns,
         verbs, adjectives, adverbs), concrete and abstract concepts, a variety of lexical fields, and different frequency ranges.

    (C2) Clearly defined. The resource must provide a clear understanding of which semantic relation exactly is annotated and measured, possibly contrasting it with other
         relations. For instance, the original SimLex-999 and SimVerb-3500 explicitly focus on true semantic similarity and distinguish it from broader relatedness captured
         by datasets such as MEN or WordSim-353.

    (C3) Consistent and reliable. The resource must ensure consistent annotations obtained from non-expert native speakers following simple and precise annotation guidelines.

- Multiple improvements have been made to the original construction protocol across several aspects such as-

      1. Coverage of more lexical fields
      2. Infrequent/rare words
      3. Focus on particular word classes
      4. Annotation quality control

- The Final Output: English Multi-SimLex. In order to ensure that the criterion C1 is satisfied, we consolidate and integrate the data already carefully sampled in prior work into a single, comprehensive, and representative dataset. This way, we can control for diversity, frequency, and other properties while avoiding to perform this time-consuming selection process from scratch. Note that, on the other hand, the word pairs chosen for English are scored from scratch as part of the entire Multi-SimLex annotation process. External data sources for the final pair of words are-

      1. SimLex-999
      2. SemEval-17
      3. CARD-660
      4. SimVerb-3500
      5. University of South Florida database

**5 Multi-SimLex: Translation and Annotation**

- This section consists of details of the development of the final Multi-SimLex resource
- Language Selection: It consists of 12 languages

    1. The main objective for our inclusion criteria has been to balance language prominence (by number of speakers of the language) for maximum impact of the resource, while simultaneously having a diverse suite of languages based on their typological features(such as morphological type and language family).
    2. There is a mixture of fusional, agglutinative, isolating, and introflexive languages that come from eight different language families.
    3. This includes languages that are very widely used such as Chinese Mandarin and Spanish, and low-resource languages such as Welsh and Kiswahili.

- The work on data can be divided into 2 crucial phases-

    1. a translation phase where the extended English language dataset with 1,888 pairs is translated into eleven target languages
    2. An annotation phase where human raters scored each pair in both translated set and English set.

  **Word Pair Translation**

- Translators for each target language were instructed to find direct or approximate translations for the 1,888-word pairs that satisfy the following rules-

    1. All pairs in the translated set must be unique (i.e., no duplicate pairs)
    2. Translating two words from the same English pair into the same word in the target language is not allowed (e.g., it is not allowed to translate car and automobile to the same Spanish word coche).
    3. The translated pairs must preserve the semantic relations between the two words when possible. This means that, when multiple translations are possible, the translation that best conveys the semantic relation between the two words found in the original English pair is selected.
    4. If it is not possible to use a single-word translation in the target language, then a multi-word expression (MWE) can be used to convey the nearest possible semantics given the above points (e.g., the English word homework is translated into the Polish MWE praca domowa).

- The quality of the translated pairs is measured by using a random sample set of 100 pairs (from the 1,888 pairs) to be translated by an independent translator for each target language.
- The sample is proportionally stratified according to the part-of speech categories.
- The independent translator is given identical instructions to the main translator; then the percentage of matched translated words between the two translations of the sample set is measured

**Data Analysis**

Similarity Score Distributions. 
- Across all languages, the average score (mean = 1:61, median= 1:1) is on the lower side of the similarity scale.
- But there are notable differences in both the averages and the spread of scores.
- All of the languages are strongly correlated with each other.
- Languages that share the same language family are highly correlated.
- We observe high correlations between English and most other languages, as expected. This is due to the effect of using English as the base/anchor language to create the dataset.
- This is a slight artifact of the dataset design.
- There is also a difference in the distribution of frequency of words among languages.
- This is related to inherent language properties. The difference can also be partially explained by the difference in monolingual corpora size used to derive the frequency rankings.
- The datasets also contain subsets of lower-frequency and rare words, which can be used for rare word evaluations in multiple languages.

Cross-Lingual Differences:

- Similarity scores range from 0 to 6. The higher the score the more similar the participants found the concepts of the pair.
- Table 7 shows evidence of stability of average scores across languages and language specific differences.
- Some differences in similarity scores seem to group languages into clusters.
- There can be many differences in the similarity scores across languages such as cultural context, polysemy, metonymy, translation, regional and generational differences, and most commonly, the fact that words and meanings do not exactly map onto each other across languages.

**Effect of language affinity on similarity scores**

- It is evident that the correlation between similarity scores across languages is not random.
- Languages from the same family or branch have similar patterns in the scores.
- In order to quantify exactly the effect of language affinity on the similarity scores, correlation analyses between these and language features is used.
- First feature vectors are extracted from URIEL. In particular, we focus on information about geography (the areas where the language speakers are concentrated), family (the phylogenetic tree each language belongs to), and typology (including syntax, phonological inventory, and phonology).
- Typological representations of languages that are not manually crafted by experts, but rather learned from texts are also considered.
- The vector for similarity judgments and the vector of linguistic features for a given language have different dimensionality. Hence, we first construct a distance matrix for each vector space, such that both columns and rows are language indices, and each cell value is the cosine distance between the vectors of the corresponding language pair.
- To estimate the correlation between the matrix for similarity judgments and each of the matrices for linguistic features, we run a Mantel test, a non-parametric statistical test based on matrix permutations that takes into account inter-dependencies among pairwise distances.
- The results show that there is a statistically significant correlation between similarity judgements and geography, family and syntax.
- The correlation coefficient is particularly strong for geography and syntax.
- Geographical proximity leads to similar judgment patterns, as mentioned above. On the other hand, we find no correlation with phonology and inventory, as expected, nor with the bottom-up typological features.

**7 Cross Lingual Multi-SimLex Dataset**

- A crucial advantage of having semantically aligned monolingual datasets across different languages is the potential to create cross-lingual semantic similarity datasets.
- Such datasets allow for probing the quality of cross-lingual representation learning algorithms as an intrinsic evaluation task.
- Compared to previous datasets this has a typologically more diverse language sample and relying on substantially larger English dataset as a source.
- The cross-lingual Multi-SimLex datasets are constructed automatically, leveraging word pair translations and annotations collected in all 12 languages.
- This yields a total of 66 cross-lingual datasets, one for each possible combination of languages.
- First, given two languages, we intersect their aligned concept pairs obtained through translation.
- The scores of cross-lingual pairs are then computed as averages of the two corresponding monolingual scores.
- Finally, in order to filter out concept pairs whose semantic meaning was not preserved during this operation; we retain only cross-lingual pairs for which the corresponding monolingual scores differ at most by one-fifth of the full scale.
- This heuristic mitigates the noise due to cross-lingual semantic shifts.

**Monolingual Evaluation of Representation Learning Models**

- This section benchmarks a series of representation learning models on the new evaluation data.
- The experiments are used to answer various questions such as –

- Is it viable to extract high-quality word-level representations from pretrained encoders receiving sub word-level tokens as input? Are such representations competitive with standard static word-level embeddings?
- What are the implications of monolingual pretraining versus (massively) multilingual pretraining for performance?
- Do lightweight unsupervised post-processing techniques improve word representations consistently across different languages?
- Can we effectively transfer available external lexical knowledge from resource-rich languages to resource lean languages in order to learn word representations that distinguish between true similarity and conceptual relatedness?

**7.1 Models in comparison**

Static Word Embeddings in Different Languages

- We evaluate a standard method for inducing non-contextualized (i.e., static) word embeddings across a plethora of different languages.
- The authors use FAST TEXT for reasons such as availability of pretrained vectors in a large number of languages, superior performance across a range of NLP tasks and its suitability for modelling rare words and morphologically rich languages.
- They use 300-dimensional FT word vectors trained on CC+ Wiki.
- The word vectors for all languages are obtained by CBOW with position-weights, with character n-grams of length 5, a window of size 5, 10 negative examples, and 10 training epochs.
- The vocabularies of all languages are trimmed to the 200K most frequent words and compute representations for multi-word phrases by averaging the vectors of the constituent words.

Unsupervised Post-Processing:

- A variety of unsupervised post-processing steps that can be applied post-training on top of any pretrained input word embedding space without any external lexical semantic resource are also used.
- The usefulness of such methods has been verified only in English
- The following post-hoc transformations are applied on the initial word embeddings-

- Mean centering (MC) is applied after unit length normalization to ensure that all vectors have a zero mean, and is commonly applied in data mining and analysis.
- All-but-the-top (ABTT) eliminates the common mean vector and a few top dominating directions (according to PCA) from the input distributional word vectors, since they do not contribute towards distinguishing the actual semantic meaning of different words.
- UNCOVEC adjusts the similarity order of an arbitrary input word embedding space, and can emphasize either syntactic or semantic information in the transformed vectors.

- All post-processing methods can be seen as unsupervised retrofitting methods that, given an arbitrary input vector space X, produce a perturbed/transformed output vector space X&#39;, but unlike common retrofitting methods, the perturbation is completely unsupervised (i.e., self-contained) and does not inject any external (semantic similarity oriented) knowledge into the vector space.
- The two hyperparameters dda (for ABBT) and α (UNOVEC) and tuned on the English Multi-SimLex and the same values are used on all the datasets. The values are dda = 3 and α = -0.3.

Contextualized Word Embeddings:

- We also evaluate the capacity of unsupervised pretraining architectures based on language modelling objectives to reason over lexical semantic similarity.
- Models such as BERT, XLM, or ROBERTA are typically very deep neural networks based on the Transformer architecture.
- They receive sub-word level tokens as inputs to tackle data sparsity. In output, they return contextualized word embeddings, dynamic representations for words in context.
- To represent words or multi-word expressions through a pretrained model, we follow prior work and compute an input item&#39;s representation by

1) Feeding it to a pretrained model in isolation

2) averaging the H last hidden representations for each of the item&#39;s constituent sub-words

3) averaging the resulting sub-word representations to produce the final d-dimensional representation, where d is the embedding and hidden-layer dimensionality (e.g., d = 768 with BERT).

- As multilingual pretrained encoders, we experiment with the multilingual BERT model (M-BERT) and XLM.
- M-BERT is trained on monolingual Wikipedia corpora of 102 languages (comprising all Multi-SimLex languages) with a 12-layer Transformer network, and yields 768-dimensional representations.
- M-BERT comprises all Multi-SimLex languages, and its evident ability to perform cross-lingual transfer also makes it a convenient baseline model for cross-lingual experiments
- XLM-100 is trained on Wikipedia dumps of 100 languages and encodes each concept into a 1280-dimensional representation.

**7.2 Results and Discussion**

- The results reported are Spearman&#39;s coefficient of the correlation between the ranks derived from the scores evaluated models and the human scores provided in each Multi-SimLex dataset.
- The main results with static and contextualized word vectors for all test languages are summarized in Table 12.
- The scores reveal several interesting patterns, and also pinpoint the main challenges for future work.

State of the art representation models:

- A general comparison between CC+Wiki and Wiki FT vectors, supports the intuition that larger corpora (such as CC+Wiki) yield higher correlations.
- A single massively multilingual model such as M-BERT cannot produce semantically rich word-level representations.
- There are differences in performance across different monolingual Multi-SimLex datasets.
- Unsupervised post-processing is universally useful, and can lead to huge improvements in correlation scores for many languages.

Impact of unsupervised post processing:

- The results suggest that applying decision wise mean centering to the initial vector spaces has positive impact on word similarity scores in all test languages and for all models, both static and contextualized.
- Applying dimension-wise mean centering has the effect of spreading the vectors across the hyper-plane and mitigating the hubness issue, which consequently improves word level similarity, as it emerges from the reported results.
- As a general rule of thumb, it is recommended to mean-centre representations for semantic tasks.
- The results further indicate that additional post-processing methods such as ABTT
- and UNCOVEC on top of mean-centred vector spaces can lead to further gains in most languages.
- Overall, the unsupervised post-processing techniques seem universally useful across languages, but their efficacy and relative performance does vary across different languages.
- In summary, pretrained word embeddings do contain more information pertaining to semantic similarity than revealed in the initial vectors.

POS-specific subsets:

- Prior work based on English data showed that representations for nouns are typically of higher quality than those for the other POS classes. A similar trend is observed in other languages as well.
- There are multiple reasons for this-

- Verb representations need to express a rich range of syntactic and semantic behaviours rather than purely referential features
- Low correlation scores on the adjective and adverb subsets in some languages (e.g., POL, CYM, SWA) might be due to their low frequency in monolingual texts, which yields unreliable representations.

- In general, the variance in performance across different word classes warrants further research in class specific representation learning.
- The scores further attest the usefulness of unsupervised post-processing as almost all class-specific correlation scores are improved by applying mean-centering and ABTT.
- Finally, the results for M-BERT and XLM-100 in Table 13 further confirm that massively multilingual pretraining cannot yield reasonable semantic representations for many languages: in fact, for some classes they display no correlation with human ratings at all.

Differences across languages:

- The results reveal that there is variation in performance of both static word embeddings and pretrained encoders across different languages.
- Among other causes, the lowest absolute scores with FT are reported for languages with least resources available to train monolingual word embeddings, such as Kiswahili, Welsh, and Estonian.
- The results also demonstrate that peak scores are achieved with different postprocessing configurations. This finding suggests that a more careful language-specific fine-tuning is indeed needed to refine word embeddings towards semantic similarity.

Multilingual vs Language Specific Contextualized Embeddings:

- We evaluate language-specific BERT and XLM models for a subset of the Multi-SimLex languages for which such models are currently available: Finnish, French, Mandarin, English and Spanish.
- We also evaluate a series of pretrained encoders available for English: (i) BERT-BASE, BERT-LARGE, and BERT-LARGE with whole word masking (WWM) from the original work on BERT, (ii) monolingual &quot;English-specific&quot; XLM and (iii) two models which employ parameter reduction techniques to build more compact encoders: ALBERT-B uses a configuration similar to BERT-BASE, while ALBERT-L is similar to BERT-LARGE, but with an 18x reduction in the number of parameters
- Monolingual pretrained encoders yield much more reliable word-level representations.
- This further confirms the validity of language-specific pretraining in lieu of multilingual training, if sufficient monolingual data are available.
- The scores obtained with monolingual pretrained encoders are on a par with or even outperform static FT word embeddings.
- This shows that such sub word-level models trained on large corpora can implicitly capture rich lexical semantic knowledge.

Similarity Specialized Word Embeddings:

- We evaluate the effectiveness of specialization transfer methods using Multi-SimLex as our multilingual test bed.
- We evaluate a current state-of-the-art cross-lingual specialization transfer method with minimal requirements (Ponti et al. 2019c).
- Semantic specialization with LI-POSTSPEC leads to substantial improvements in correlation scores for the majority of the target languages, demonstrating the importance of external semantic similarity knowledge for semantic similarity reasoning.
- we also observe deteriorated performance for the three target languages which can be considered the lowest-resource ones in our set: CYM, SWA, YUE.
- We hypothesize that this occurs due to the inferior quality of the underlying monolingual Wikipedia word embeddings, which generates a chain of error accumulations.
- Poor distributional word estimates compromise the alignment of the embedding spaces, which in turn results in increased translation noise, and reduced refinement ability of the relation classifier.
- Typological dissimilarity between the source and the target does not deteriorate the effectiveness of semantic specialization.

**8 Cross-Lingual Evaluation**

**8.1 Models in comparison**

Static word embeddings:

- A state-of-the-art mapping-based method for the induction of cross-lingual word embeddings (CLWEs): VECMAP
- The core idea behind such mapping-based or projection-based approaches is to learn a post-hoc alignment of independently trained monolingual word embeddings.
- They support CLWE induction with only as much as a few thousand-word translation pairs as the bilingual supervision.
- Recent empirical studies have compared a variety of unsupervised and weakly supervised mapping-based CLWE methods, and VECMAP emerged as the most robust and very competitive choice.
- Therefore, we focus on 1) its fully unsupervised variant (UNSUPER) in our comparisons. For several language pairs, we also report scores with two other VECMAP model variants: 2) a supervised variant which learns a mapping based on an available seed lexicon (SUPER), and 3) a supervised variant with self-learning (SUPER+SL) which iteratively increases the seed lexicon and improves the mapping gradually.
- Again CC+Wiki FT vectors are used as initial monolingual word vectors.

Contextualized Cross-Lingual Word Embeddings:

- We again evaluate the capacity of (massively) multilingual pretrained language models, M-BERT and XLM-100, to reason over cross-lingual lexical similarity.
- We rely on the same procedure of aggregating the models sub word-level parameters into word-level representations.

  **Results**

Main Results and Differences across Language Pairs –

- A summary of the results on the 66 cross-lingual Multi-SimLex datasets are provided in Table 15 and Figure 6a.

- We observe that the fully unsupervised VECMAP model, despite being the most robust fully unsupervised method at present, fails to produce a meaningful cross lingual word vector space for a large number of language pairs.
- Many correlation scores are in fact no-correlation results, accentuating the problem of fully unsupervised cross-lingual learning for typologically diverse languages and with fewer amounts of monolingual data
- The scores are low for low resource languages like Welsh.
- It also seems that the lack of monolingual data is a larger problem than typological dissimilarity between language pairs.
- Typological differences (e.g., morphological richness) still play an important role as we observe very low scores when pairing CMN with morphologically rich languages such FIN, EST, POL, and RUS.
- The scores of M-BERT and XLM-100lead to similar conclusions as in the monolingual settings.
- The scores indicate a much higher performance of language pairs where YUE is one of the languages when we use M-BERT instead of VECMAP. This boils down again to the fact that YUE, due to its specific language script, has a good representation of its words and sub words in the shared M-BERT vocabulary.
- The results also verify the usefulness of unsupervised postprocessing also in cross-lingual settings.

Fully Unsupervised vs. Weakly Supervised Cross-Lingual Embeddings

- The results indicate that fully unsupervised cross-lingual learning fails for a large number of language pairs.
- We examine 1) if we can further improve the results on cross-lingual Multi-SimLex resorting to (at least some) cross-lingual supervision for resource-rich language pairs; and 2) if such available word-level supervision can also be useful for a range of languages which displayed near-zero performance.
- We reassess the findings established on the bilingual lexicon induction task: using at least some cross-lingual supervision is always beneficial compared to using no supervision at all.
- We report improvements over the UNSUPER model for all 10 language pairs in Table 16, even though the UNSUPER method initially produced strong correlation scores.
- The importance of self-learning increases with decreasing available seed dictionary size, and the +SL model always outperforms UNSUPER with 1k seed pairs.
- The results also indicate that at least some supervision is crucial for the success of static CLWEs on resource-leaner language pairs.

Multilingual vs. Bilingual Contextualized Embeddings

- The paper compares the 100-language XLM-100 model with

1. A variant of the same model trained on a smaller set of 17 languages (XLM-17)
2. A variant of the same model trained specifically for the particular language pair (XLM-2)
3. A variant of the bilingual XLM-2 model that also leverages bilingual knowledge from parallel data during joint training (XLM-2++).

- The results confirm the intuition that massively multilingual pretraining can damage performance even on resource-rich languages and language pairs.
- A rise in performance is observed when the multilingual model is trained on a much smaller set of languages (17 versus 100), and further improvements can be achieved by training a dedicated bilingual model.
- Finally, leveraging bilingual parallel data seems to offer additional slight gains, but a tiny difference between XLM-2 and XLM-2++ also suggests that this rich bilingual information is not used in the optimal way within the XLM architecture for semantic similarity.

- In summary, these results indicate that, in order to improve performance in cross lingual transfer tasks, more work should be invested into

1) pretraining dedicated language pair-specific models

2) creative ways of leveraging available cross-lingual supervision with pretrained paradigms such as BERT and XLM.

- Using such cross-lingual supervision could lead to similar benefits as indicated by the results obtained with static cross-lingual word embeddings.
