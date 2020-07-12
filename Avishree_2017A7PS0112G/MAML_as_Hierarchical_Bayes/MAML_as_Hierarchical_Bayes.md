# Recasting Gradient-based Meta-Learning as Hierarchical Bayes

Created: Jul 12, 2020 11:49 AM

Description: Establish MAML as an approximation of Hierarchical Bayesian Inference

Materials: https://arxiv.org/pdf/1801.08930.pdf

Status: In progress

### To do

- [ ]  Include the math used for proving equivalence

### Meta-Learning and Inductive Bias

Meta-Learning is formulated as the extraction of domain-general information that can act as an inductive bias to improve learning efficiency in novel tasks.

**How is this inductive bias implemented?**

1. As learned hyperparameters in a hierarchical Bayesian model that regularize task-specific parameters.
2. As a learned metric space in which to group neighbours.
3. As a trained recurrent neural network that allows encoding and retrieval of episodic information.
4. As an optimization algorithm with learned parameters (MAML falls in this category)

### MAML and inductive bias

1. MAML is a learned optimization procedure that directly optimizes the standard gradient descent rule.
2. The algorithm estimates an initial parameter set to be shared among the different tasks.
3. The intuition is that gradient descent from the learned initialization provides a favourable inductive bias for fast adaptation.

### What does the paper claim?

The paper claims that MAML approximates hierarchical Bayesian inference in the sense that the meta-parameters learned during training represent a prior on the tasks (a task-general prior). Hence, when given a new task to learn from, even with limited data and computation, the model is quickly able to adapt the parameters for optimum performance on the new task.

(I have for now omitted the math used to prove the equivalence)