# BERT-Goldberg paper

## BERT model:

BiDirectional Encoder representations from Transformers

12/24 encoder layers (Transformer blocks) in BERT base

Context of a word known from all surroundings (both left and right)

Training strategies: 

- MLM: predict masked based on non-masked and context
- NSP: pair of sentences as input, predict if second one is subsequent to the first one

## Aim of Paper:

To check if BERT captures syntax sensitivity. Methods used for checking:

- **subject-verb agreement** stimuli
- **colorless green ideas**
- manually: SVA and "**reflexive anaphora phenomena**" *

*what is this? → [https://en.wikipedia.org/wiki/Anaphora_(linguistics)](https://en.wikipedia.org/wiki/Anaphora_(linguistics))

(reflexive → ends with "self)

Negative Polarity Items: English words like ANY, EVER

## Implementation:

Prefix sentence -  [mask] - suffix sentence

PyTorch implementation, pretrained models from Google used.

## Other Definitions:

- Sentential Complement Verbs: These verbs require an entire sentence to come after them. This sentence has its own rules independent from the sentential complement verb.
- Short/Long VP coordination: Coordinator joins two VPs. For example, "The president will **[understand** **the criticism]** and **[take action]**." - VP + VP

Link to the paper: [https://arxiv.org/abs/1901.05287](https://arxiv.org/abs/1901.05287)
