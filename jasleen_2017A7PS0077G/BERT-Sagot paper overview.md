# BERT-Sagot paper

## Aim of the paper:

Assessing the elements of English language structure learned by BERT. 

- phrasal information captured in lower layers
- intermediate layers encode heirarchical linguistic information:
    - *bottom: surface features (form, shape, structure?)*
    - *middle: syntactic features*
    - *top: semantic features*

Subject-verb agreement requires deeper layers required by BERT to capture long-distance dependencies

## Implementation of BERT used:

Pytorch based "bert-based-uncased" variant whose details are as:

- 12 layers each having a hidden size of 768 and 12 attention heads (110m parameters)

## Phrasal Syntax:

LSTM-based language models can capture phrase(span) level information. 

Aim: To check if this applies to BERT as well

Extract span representations from each layer of BERT.

"*For a token sequence Si, ..., Sj , we compute the span representation S(Si,Sj),l at layer l
by concatenating the first (H Si, l) and last hidden vector (H Sj, l) along with their element-wise product and difference.*"

Results: Lower layers have more phrasal information

## [Probing Tasks:](https://nlp.stanford.edu/~johnhew/interpreting-probes.html)

"*If an auxiliary classifier can predict a linguistic property well, then the original model likely encodes that property."*

For each layer of BERT, 10 tasks which are grouped into 3 categories: 

- Surface task: sentence length, presence of words
- Syntactic task: sensitivity to word order, the depth of the syntactic tree, the sequence of top
level constituents in the syntax tree
- Semantic task: check for the tense, subject number in main clause, the sensitivity
to random replacement of a noun/verb and the random swapping of [coordinated clausal conjuncts.](https://www.grammarly.com/blog/coordinating-conjunctions/#:~:text=A%20coordinating%20conjunction%20is%20a,or%2C%20yet%2C%20and%20so.)

## Subject-verb agreement:

Performing the test on each layer, and increasing the number of attractors.

Result: "*As the number of attractors increases, one of the higher BERT layers (#8) is
able to handle the long-distance dependency problems caused by the longer sequence of words intervening between the subject and the verb, better than the lower layer (#7)."*

## Compositional Structures:

[Tensor Product Decomposition Networks](https://rtmccoy.com/tpdn/tpr_demo.html)

For each BERT layer, 5 role schemes used: **1)** left-to-right index   **2)** right-to-left index   **3)** ordered pair of left-to-right and right-to-left indices   **4)** position in syntactic tree   **5)** index common to all the words in the sentence (ignoring its position) 

Results: BERT encodes tree-like structures despite using attention mechanisms.

Link to the paper: [https://www.aclweb.org/anthology/P19-1356/](https://www.aclweb.org/anthology/P19-1356/)
