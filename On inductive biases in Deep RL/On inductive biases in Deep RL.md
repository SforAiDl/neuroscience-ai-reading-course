# On inductive biases in Deep RL

Matteo Hessel, Hado van Hasselt, Joseph Modayil, David Silver

[https://arxiv.org/pdf/1907.02908.pdf](https://arxiv.org/pdf/1907.02908.pdf)

## Key Takeaways

- Inductive biases in DRL include domain knowledge and hyperparameter tuning
- Strong biases can lead to faster training, but weak biases can lead to generality
- Two of such methods are compared on a continuous control task. Turns out that the adaptive (More General) method performs better - Acting as a critic for biases in Deep RL
- The authors used a tabular A2C method, with the best hand tuned parameters, compared to a meta-gradient algorithm (for better generalization)

## Common biases and their counterparts

### Sculpting the objective

- The same learning rate and other hyperparameters can not be used for different task, since updates scale linearly with the return
- Hence - reward clipping - between -1 and 1
- Problem - if all non zero positive rewards are >1 : leads to maximising the frequency of rewards, and not their cummulative sum
- Look at [PopArt](https://arxiv.org/abs/1809.04474) - used for better adaptation to reward scaling
- Discounting - Training might be faster, but may lead to faster training but more myopic performance, at the cost of an extra hyperparameter
- Meta gradient algorithms may be used to learn this hyperparameter, given the setting

### Sculpting the agent-environment interface

- What time scale should the agent learn at??
- Slower time scales can be beneficial - appropriate ranking of actions using noisy estimates may lead to stable learning, computational costs can be saved, back and forth jittering of actions has been eradicated - may lead to exploration
- A very general solution - Let the agent learn at what time scale it should learn in
- A simpler solution - output actions $A_t$  and $C_t$  (commitment) from different policies
- Previously - scaling the Atari image down from 210x160 to 84x84, grayscaling, and concatenating 4 frames
- What the authors did - Feed the RGB Pixels into 2 conv layers(32 and 64 channels resp, kernel size = 5x5, stride = 5), Linear(256) and LSTM. The outputs $A_t$ and $C_t$ are computed as logits coming from two different linear layers from the LSTM

## Experiments and results

- All the performances are measured in average reward over the previous n timesteps
- Selecting the discount factor - May be really tough to narrow down, authors came to a conclusion that 0.5-0.9 is the best range. The adaptive algorithm learnt and performed at par to the best hand tuned value even when it was initialised to 0.95
- Reward scaling - The adaptive algorithm performed better than carefully hand tuned learning rate, for a discount factor of 0.8 (best from the prev experiment)
- Number of action repeats - 11 cyclic states, +100 reward if there is constant action selection in the 11 state. The A2C learns to chose the number of repititions, the adaptive algorithm quickly learnt it, performing better than the tabular A2C

![https://github.com/hades-rp2010/neuroscience-ai-reading-course/blob/master/On%20inductive%20biases%20in%20Deep%20RL/imgs/Untitled.png](https://github.com/hades-rp2010/neuroscience-ai-reading-course/blob/master/On%20inductive%20biases%20in%20Deep%20RL/imgs/Untitled.png)

### Large Domain performance

- Agents were trained on 57 Atari games. The adaptive algorithm performs at par with the fine tuned agents in most of the biases that it accounts for
- Action Repeats - 3 agents: one is the adaptive agent, another is handtuned, and third acts at the fastest timescale(least commitment)
- The adaptive and the handtuned agent perform at par, the fastest timescale agents performance plateus for several games
- Disounting - 3 agents: handtuned, adaptive, and no discounts. The no discounts agent performs poorly as compared to the other two, which were at par with each other
- Reward scaling - 3 agents: Clipping the rewards, PopArt, no clipping. Here the performances are in the order clipping, PopArt, and then no clipping
- The reason might be that clipping the rewards (maximise the frequencyof greater than 1 rewards) acts as a good proxy for many of the Atari games
- Learning from raw observations - The outcome shows that the adaptive algorithm is powerful enough to learn the relevant features on its own, performing better than an agent with handcrafted features.

![https://github.com/hades-rp2010/neuroscience-ai-reading-course/blob/master/On%20inductive%20biases%20in%20Deep%20RL/imgs/Untitled%201.png](https://github.com/hades-rp2010/neuroscience-ai-reading-course/blob/master/On%20inductive%20biases%20in%20Deep%20RL/imgs/Untitled%201.png)

### Performance on Unseen tasks

- The Deepmind continuous control suite was used for these tasks. No convolutions were used in the network due to lack of spatial features, and outputs were interpreted as encoding the mean and variance instead of cateogrical logits. The results are shown below

![https://github.com/hades-rp2010/neuroscience-ai-reading-course/blob/master/On%20inductive%20biases%20in%20Deep%20RL/imgs/Untitled%202.png](https://github.com/hades-rp2010/neuroscience-ai-reading-course/blob/master/On%20inductive%20biases%20in%20Deep%20RL/imgs/Untitled%202.png)

## Further ideas

- This work is a critic of inductive biases being used. There is evidence that [humans use inductive biases](https://arxiv.org/abs/1802.10217) that lead to efficient learning, there might be a connection here
- A combination of both - inductive and general learning, similar to humans, the DRL agent gets to chose between taking an inductive step and learning from that, or taking a more general step
