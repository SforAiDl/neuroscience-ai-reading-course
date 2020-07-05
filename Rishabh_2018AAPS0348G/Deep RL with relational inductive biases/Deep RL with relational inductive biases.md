# Deep RL with relational inductive biases

Vinicius Zambaldi, David Raposo, Adam Santoro

[https://openreview.net/pdf?id=HkxaFoC9KQ](https://openreview.net/pdf?id=HkxaFoC9KQ)

## Key takeaways

- The authors augment model free RL with the ability to relationally reason over structured representations - improving the performance, generalization, efficiency, interpretability
- The agent encodes the input state(image) as a set of vectors, and iteratively passes messages to identify and reason about relevant entities in a scene, and their relations
- Examining this agents learned representations captured the structure of the problem, and the agents intentions. It was also able to generalise over more complex scenes than encountered in training
- Such reasoning over relations can lead to better generalizations over unseen states, or more complex environments with the same dynamics, as the authors do with starcraft2LE

## Relational DRL agent architecture

- Started off with a distributed A2C and then produced some ***relational*** changes to it
- Input module -
    - Inputs are images passed through a CNN to get a set of embedded representations S
    - This S (size mxnxf) is then flattened to (Nxf, where N = mxn) - A set of entity vectors, so that each row of E, $e_i$ corresponds to a feature vector $s_{x, y}$ a paritcular x,y location in the embedded scene - Helps [non local computations](https://arxiv.org/pdf/1711.07971.pdf) between entities for relations
- Relational module -
    - For one step of relational computation, the pairwise interactions between all the enities, including self, is calculated, using a multi-head dot product attention mechanism (MHDPA)

    ![https://github.com/hades-rp2010/neuroscience-ai-reading-course/blob/master/Rishabh_2018AAPS0348G/Deep%20RL%20with%20relational%20inductive%20biases/Deep%20RL%20with%20relational%20inductive%20biases/Untitled.png](https://github.com/hades-rp2010/neuroscience-ai-reading-course/blob/master/Rishabh_2018AAPS0348G/Deep%20RL%20with%20relational%20inductive%20biases/Deep%20RL%20with%20relational%20inductive%20biases/Untitled.png)

    - Similarities between query $q_i$ and all the keys $k_{j = i:N}$ are computed via dot product, and normalised to attention weights via softmax
    - Pairwise interaction terms are then calculated as $p_{i,j} = w_{i,j}v_j$ and summing these as $a_{i}=\Sigma_{j=1:N}a_{i, j}$ act as attention weights
    - The updates to entities are then calculated by concatenating the attention weights, passing them through an MLP, and adding them to the entity vectors
    - This one step is called a "block" and can be applied iteratively to compute higher order interactions, similar to GNNs
- Output modules
    - The output from the previous model is a matrix E of shape (Nxf). Maxpooling applied on the entity dimension, outputing an f dimensional vector
    - This is then passed through an MLP, giving (c+1) outputs, c actions and 1 for the state value

### Experiments and results

- Box world -
    - A hypothetical scenario where one open key (color coded) exists, and it can be used on a lock with the same color. Each lock corresponds to a box having either another key of some color, or a gem. Obtaining the gem wins the episode, whereas opening a wrong lock destroys the key, reaching a dead end
    - The main branch (leading up to the gem) had its length varied form 1 to 4, same with the distractor branch (branches leading to a dead end)
    - Agents with the relational module were able to solve 98% of the tasks, the longer the distraction branch, more the number of relational blocks required (to compute higher order relational computations)
    - Baseline agent (using only conv layers), an A3C agent, and a distributed Q learning agent with prioritized replay were able to solve less than 75% of the tasks
    - The baseline agent performs much better with a backward branch, implying its poor performance can be attributed to its lack of reasoning capability
    - Analysis of attention weights - Arrows point from the source to the what it is attending

    ![https://github.com/hades-rp2010/neuroscience-ai-reading-course/blob/master/Rishabh_2018AAPS0348G/Deep%20RL%20with%20relational%20inductive%20biases/Deep%20RL%20with%20relational%20inductive%20biases/Untitled%201.png](https://github.com/hades-rp2010/neuroscience-ai-reading-course/blob/master/Rishabh_2018AAPS0348G/Deep%20RL%20with%20relational%20inductive%20biases/Deep%20RL%20with%20relational%20inductive%20biases/Untitled%201.png)

    - The paper suggested 4 relations -
        - The keys attend to the locks that can be unlocked with it
        - The locks attend to the keys that can be used to unlock it
        - All the objects attend to the agents location
        - The gem and the agent attend to each other
    - If the agent does actually learn the notion of unlock(lock, key), then the length of the sequence, and pairs it has not seen before shouldnt make a difference. The authors tested the relational agents ***without further training*** on both of these scenarios, and it performed significantly better (88% and 97%) resp, as opposed to a non relational agent (5% and 13%) - Can be thought of as ***zero shot transfer*** to more complex tasks

- Starcraft 2 Learning environment -
    - Changes to the agent architecture
        - Uses 2 sets of residual conv blocks, each having 3 conv layers each
        - 2D conv LSTM layers were added, to account for the history of actions/observations, and partially observable states - another reason might be that the orders are issued to agents over multiple time steps, if not, this may lead to the agent issuing the same order repeatedly instead of issuing other orders to other units
    - The relational agent beats a human grandmaster in 4 of the 7 games, and achieves SOTA in 6 of the 7 games
    - This might be due to better RL algorithms, more robust architecture and better hyperparameter tuning, leading to better credit assignment, exploration, action selection procedures
    - Generalization Capabilities - the agent had previously been trained on 2 units to mine emaralds. Catch is, these 2 units can be controlled independently, which the relational agent learns. Being tested on 10 units, the control agent performs a forward sweep - trying to cover max area by all the 10 agents, whereas the relational agent uses these 10 units simultaneously to maximise its score

## Further Ideas

- Such relational modules can be used to turn the problem from a model free to a model based RL problem - then the application of the bellman equations can provide us the optimal solution

## Further Readings

- [Relational Forward models for multi agent learning](https://arxiv.org/pdf/1809.11044.pdf)
