# Visually Grounded Neural Syntax Acquisition

[Shi et al. ACL 2019 Visually Grounded Neural Syntax Acquisition](https://arxiv.org/abs/1906.02890)

Visually Grounded Neural Syntax Learner (VG-NSL) is an approach for learning syntactic representations and structures without explicit supervision. The modellearns by looking at natural images and reading paired captions. VG-NSL generates constituency parse trees of texts, recursively composes representations for constituents, and matches them with images.

## Intuition
Consider the figure below paired with the descriptive texts (captions) in English. Given no prior knowledge of English, and sufficient such pairs, one can infer 
- the correspondence between certain words and visual attributes, (e.g. recognizing that “a cat” refers to the objects in the blue boxes).
- constituents, that is a set of consecutive words to be processed as a whole (e.g. "A cat", "under the umbrella")

![](https://github.com/bhatiakartik10/neuroscience-ai-reading-course/blob/master/Kartik_2017A7PS0051G/Visually%20Grounded%20Neural%20Syntax%20Acquisition/1.jpg?raw=true)

This intuition motivates the use of image-text pairs to facilitate automated language learning, including both syntax and semantics. 
This paper focuses on learning the syntactic structures, and proposes Visually Grounded Neural Syntax Learner (VG-NSL) that acquires syntax, in the form of constituency parsing, by making use of images and their captions.

## Methodology

VG-NSL consists of 2 modules.
1. Given an input caption, build a constituency parse tree, and recursively compose representation for every constituent. 
2. Match textual representations with visual inputs, using Visual-Semantic embeddings. 
Both are jointly optimized in an alternating mechanism.

![](https://github.com/bhatiakartik10/neuroscience-ai-reading-course/blob/master/Kartik_2017A7PS0051G/Visually%20Grounded%20Neural%20Syntax%20Acquisition/2.jpg?raw=true)

### Textual Representation and Structures

- VG-NSL starts by composing a binary constituency structure of text, using an easy-first bottom-up parser.
- The composition of the tree from a caption of length n consists of n-1 steps. of n− 1 steps. Let X(t) = (x1(t), x2(t), · · · , xk(t)) denote the textual representations of a sequence of constituents after step t, where k = n − t. X(0) to denote the word embeddings for all tokens (the initial representations).
- The selected pair is combined to form a single new constituent. Thus, after step t, the number of constituents is decreased by 1. The textual representation for the new constituent is defined as the L2-normed sum of the two component constituents.

![](https://github.com/bhatiakartik10/neuroscience-ai-reading-course/blob/master/Kartik_2017A7PS0051G/Visually%20Grounded%20Neural%20Syntax%20Acquisition/3.jpg?raw=true)

### Visual-Semantic Embeddings

- Visual-semantic embedding (VSE) space for paired images and text constituents. Let v(i) denote the vector representation of an image i, and c(i)j denote the vector representation of the j-th constituent of its corresponding text caption.
- A function m(.; .; phi) is defined as the matching score between images and texts:

![](https://github.com/bhatiakartik10/neuroscience-ai-reading-course/blob/master/Kartik_2017A7PS0051G/Visually%20Grounded%20Neural%20Syntax%20Acquisition/7.jpg?raw=true)





