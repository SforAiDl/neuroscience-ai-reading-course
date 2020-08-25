# Universal linguistic inductive biases via meta-learning

Created: Aug 25, 2020 10:40 AM
Description: How do you impart certain universal inductive biases to a linguistic model
Materials: https://arxiv.org/pdf/2006.16324.pdf
Status: Done reading

**How does one learn a new language?**

Data + Inductive bias

**What is this inductive bias?**

These are factors that help the learner generalize beyond the particular examples from the data

**How can you model the inductive biases?**

1. Probabilistic modelling (have a structure defined)
    - Quite constrained and can only learn a specific set of language
2. Neural-network based modelling (learn the structure based on the data)
    - Although these can learn many languages, there are no constraints on the kinds of biases imparted (and so, their inductive biases can be very different from those that humans possess)

    **This paper presents a framework that can impart certain required inductive biases to the model's initial state using meta learning***

**The Framework**

1. Select a set of inductive biases that you wish to impart to the model
2. Construct a set of languages having the given inductive biases and use this set to train the model using meta-learning
3. Present new languages to the model and verify if the model has learnt the inductive biases in predicting outputs for the new languages

**Results**

The model trained using meta-learning was found to use the inductive biases even when trained on very few samples from the new language. The model was proved to not be memorizing the data points from the training set by presenting it with languages that only contained some of the inductive biases (performed well on these too!)

**How can this be useful?**

1. We can build models with a set of inductive biases that we wish for it to have.
2. We can use meta-learning to train on natural languages and then infer the kinds of inductive biases it manages to learn.