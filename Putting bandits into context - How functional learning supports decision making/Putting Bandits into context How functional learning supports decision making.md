# Putting Bandits into context: How functional learning supports decision making
Eric Schulz, Emmanouil Konstantinidis, Maarten Speekenbrink
[https://https://pubmed.ncbi.nlm.nih.gov/29130693/](https://https://pubmed.ncbi.nlm.nih.gov/29130693/)
## Key Takeaways

- CMAB to investigate learning in uncertain environments
- Learning the context reward function is pretty easy if the function is linear, whereas most participants resort to the blind (non-contextual) mean strategy when the function is non-linear
- Most of the participants behaviour can be described by a Gaussian process (with LR → the contextual learning approach
- No linearity bias present - may be because of the decision making paradigm and not the prediction paradigm

## CMAB framework

- At each time step, the agent is provided with a context, and a set of choices, whode expected reward is dependent on the context via an unknown function
- Rewards are stochastic, implying a gamble even if the agent has complete knowledge of the environment
- Context blind decisions - a restless bandit task, since the rewards keep chamging as the context changes, even for the same choice
- Contextual decisions - Make learning the function easier, hence optimal arm selection for max reward becomes relatively easier

## Learning Models

- Rule based - poeple learn functions by assuming it belongs to an explicit parametric form, eg - Linear, polynomial, exp. Prob - ignores how people chose from this set
- Similarity based - associate similar inputs to similar outputs. Prob - cant explain how people generalise when inputs provided are not similar
- EXtrapolation Association Model (EXAM) - similarity based for interpolation, linear for extrapolation, cant explain non linear extrapolation
- POpulation of Linear Experts (POLE) - knowledge partitioning, learn different functions for different sets of inputs, and then stitch them together

### Gaussian process regression

- A marginal distributional over all functons

### Context blind learning

- Bayesian mean tracking - $p(\mu_j|D_{t-1}) = N(m_{j, t}, v_{j,t})$
- Kalman filter - assumes a time varying mean instead of a stationary mean $\mu_{j, t+1} + \mu_{j, t} + \epsilon_t$ where $\epsilon_t = N(0, \sigma_{\epsilon}^2)$
- The mean and the variance then are updated as $m_{j,t} = m_{j, t-1} + \delta_{j, t}G_{j, t}(y_t - m_{j, t-1})$ where $G_{j, t}$  is the Kalman gain. Similarly $v_{j, t}= (1-\delta_{j, t}G_{j, t})(v_{j, t-1} + \sigma_{\epsilon}^2)$

### Decision Strategies

- 4 are used - UCB, POI, EI, PMU
- POI - probability of improvement: estimated the probability that another arm can give a better reward given the context than the previous arms
- EI - Epected improvement: Like POI except considers the amount of improvement as well
- PMU - Prob of maximum utility: estimates the probability that a given arm will give the maximum reward given the context

## Experiments

- All models are compared on the basis of their out of sample 1 step lookahead prediction, as compared to a random sample
- For all (t-1) trials, the data is fitted with a differential evolution algorithm for each of the participants

### Exp1 - Binary contexts

- 3 contexts are provided, binary, can be -1 or +1
- Three of the functions are linear in these contexts, and one does not depend on the context, Designed such that the expected reward over all functions is 50
- To get a better then 50 reward, participants have to learn about the function mapping
- Participants tend to learn context dependence, achieveing a mean reward of 68, best captured by an RBF kernel in a GP, and using the POI strategy
- Frequency of selecting the non contextual arm reduces over time
- May have occured via memorization due to the small number of contexts (8)

### Exp2 - Continuous Linear contexts

- 3 contexts, non binary, can be in the range (-10, 10), making memorizing more difficult
- Same type of function dependence on contexts
- Frequency of selecting the non contextual arm did not decrease significantly over time, but the frequency of selecting the optimal arm did increase
- The contextual models in this case, did not significantly outperform the context blind models
- Contextual behaviour is best described by the RBF Kernel, using UCB, context free by the PMU method
- Participants, some of them, do seem to learn the differential dependence the contexts have on the reward

### Exp3 - Continuous Non-Linear Contexts

- Non linear functions in this case were sampled from a GP prior, else the task remained the same
- Participants in this case are only 1.2 times more likely to exhibit contextual learning as opposed to contex-blind learning, may be because of the increased complexity
- Significant increase of score wrt trial is not substantial(0.3 times more likely), and the frequency of selecting the non contextual arm does not decrease significantly with time(0.1 times more likely)
- Same as the previous task, the contextual models did not significantly outperform the context blind models
- Contextual behaviour best described by RBF + UCB, PMU for non contextual

### Parameter analysis

- Shows that there is negative correlation between exploration and complexity of the task
- Participants approach all three tasks with the same assumptions of smoothness of the function (length scale param in RBF kernel)

## Further Ideas

- Reward function can be taken to incorporate the cost of taking wrong actions - may lead to careful and accurate learning, but may also lead to less exploration
- Context dependence was the same for all in this case. There can be a scenario where there are general as well as specific features as contexts (Multicontextual)
- Multifunctional Multicontextual - something like a composition of functions of each context affects the reward can be looked into

##Read ahead

- [Exploration-exploitation in contextual multi arm bandit tasks](https://http://cpilab.org/pubs/Schulz2015exploration.pdf)
