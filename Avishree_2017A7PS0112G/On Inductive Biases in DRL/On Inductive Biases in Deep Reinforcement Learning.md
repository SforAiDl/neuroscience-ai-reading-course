# On Inductive Biases in Deep Reinforcement Learning

Created: Jul 3, 2020 2:46 PM
Description: Adaptive systems (weak inductive bias) vs. domain heuristics (strong inductive bias) performance comparison and related discussion
Materials: https://arxiv.org/pdf/1907.02908.pdf
Reviewed: No
Status: In progress

### Reinforcement Learning today

- Human-level performance is surpassed by RL agents in several challenging tasks (Go, Chess, Atari, etc.).
- Most of these models are explicitly tuned for the particular task, and substantial effort is required to collect the required domain-specific knowledge and tune hyperparameters.
- Hence, these agents cannot do well on new tasks presented to them.

### AlphaZero

- AlphaZero removed dependencies on all inductive-biases and data related to the game of Go.
- It not only achieved higher performance on Go but also learned how to play Chess and Shogi (effectively).

### Performance vs. Generality

Strong inductive biases lead to faster training and better performance on the given task. On the other hand, weak inductive biases lead to more general algorithms than can adapt to many new tasks.

### The problem with inductive biases

- As mentioned above, strong inductive biases lead to "specific" algorithms that will not generalize well on new tasks.
- Also, collecting inductive biases in the form of domain-knowledge and pretuned parameters is a time and effort consuming task.

### About this paper

Replace common domain heuristics with adaptive components and report the differences. The domain heuristics considered are as follows:

1. Those that sculpt the agent's objective
2. Those that sculpt the agent-environment interface

There were several adaptive components experimented in the paper. I'd like to however focus on the one involving meta-learning.

### Important Conclusions

1. The adaptive components can replace carefully crafted domain heuristics and still achieve comparable results (with respect to ALE).
2. No additional tuning is required to train these adaptive systems (actor-critic agents) on new continuous control tasks. These agents, indeed, outperform agents that were specifically tuned for these tasks.

### Meta-Learning

One of the adaptive components introduced was the use of meta-learning to tune the discount factor ($\gamma$). In traditional settings, $\gamma$ is tuned manually. The paper compares this against using adaptive [meta-learning](https://arxiv.org/pdf/1805.09801.pdf) to learn the parameter $\gamma$. 

**A note on discount factor:** Discount factor is a rather sensitive hyperparameter. It is hence tuned manually to various values to decide the optimum value. Undiscounted rewards are not common as adding discounts helps in easier learning where the agent can focus on a relatively short time horizon.

### Experiment

**Problem setting**

Consider a chain environment with $T = 9$ states and 2 actions (moving left and right). The reward associated with moving left is -1 and is $2d / T$ otherwise (where $d$ is the distance from the left end). Hence, the objective of the agent is to reach the right end which is when it is given an additional reward of $T$.   

**Discount factor**

It was found that the best performance was obtained when $\gamma$ was in the range of 0.5 to 0.9. Hence, setting lower or higher values resulted in poor performance. Note that using undiscounted returns ($\gamma = 1$) would also result in poor performance. 

**Meta-Learning vs. Fixed discount**

The paper shows that using meta-learning to find the parameter $\gamma$ was very effective. Even when initialized to a value of 0.95, the agent learned to reduced the value and performed at par with the best tuned fixed discount.

![On%20Inductive%20Biases%20in%20Deep%20Reinforcement%20Learning%20579218bedc8545e18bd22af0e79b105f/inductive-biases-drl-av-reward.png](On%20Inductive%20Biases%20in%20Deep%20Reinforcement%20Learning%20579218bedc8545e18bd22af0e79b105f/inductive-biases-drl-av-reward.png)

Average step reward for various values of discount factor

![On%20Inductive%20Biases%20in%20Deep%20Reinforcement%20Learning%20579218bedc8545e18bd22af0e79b105f/inductive-biases-drl-comparison.png](On%20Inductive%20Biases%20in%20Deep%20Reinforcement%20Learning%20579218bedc8545e18bd22af0e79b105f/inductive-biases-drl-comparison.png)

Comparison of various algorithms on tuning discount parameter