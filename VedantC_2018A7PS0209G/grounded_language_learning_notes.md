# Grounded Language Learning 

### What is GLL?

GLL is a way to teach language to machines the same way humans do, which is through a non-linguistic experience of the real world.  

Idea - Intuitively, language can be better learned when presented and interpreted in the context of the world it pertains to.

Human language does not exist in isolation; it is learned, understood, and applied in the physical world in which people exist. Understanding symbols and symbolic reasoning has been a core element of artificial intelligence throughout the history of the field. Finding the connection between those symbols and their underlying meanings is the grounded language acquisition problem: taking linguistic tokens and learning to interpret them by connecting them to real-world percepts and actions.

Language is grounded in experience. Unlike dictionaries which define words in terms of other words, humans understand many basic words in terms of associations with sensory-motor experiences. People must interact physically with their world to grasp the essence of words like "red," "heavy," and "above."
Abstract words are acquired only in relation to more concretely grounded terms. Grounding is thus a fundamental aspect of spoken language, which enables humans to acquire and to use words and sentences in context.

For a good overview of GLL, I would recommend reading the paper - https://www.ijcai.org/Proceedings/2018/0810.pdf

### How can we make machines learn like humans do?

The idea is to make models learn by mapping one or more input modalities to the other. So for example making a model learn what the word “car” means by showing it images of cars and maybe also some audio of what a car sounds like. So that the model has a real world understanding of a car. We associate car images and audio sounds to the word “car”.

And, to interpret language in context of a world, other modes of input are also involved in GLL such as Olfactory Perception and Haptic feedback.

Classification algorithms have been shown to be successful in learning language this way like different types of neural networks for example.

### Language as Classification 

In a statistical approach the key question is What underlying knowledge representation should be used to represent groundings? In a lot of GLL problems, a key insight is that understanding words and phrases can be conceptualized as a classification problem. So, when language references physical objects or actions, words and linguistic structures may be considered a classifier.

### A simple approach to train grounded language classifiers.

In this overview, perceptually-derived world information, or context C, is interpreted by a perceptual model that encodes the kind of knowledge that the system is expected to learn—in this case features representing color and shape. An encoding of some particular context gives a formal, perceptual world representation w. Similarly, a language model (here, a learned semantic parser) is applied to a natural language utterance x in order to produce a formal semantic meaning representation, z.

The language model P(z|x) and perception model P(w|C) are trained independently, but then a joint probability is specified by coupling them with a grounding G, given by P(G|z, w), a conditional probability term that holds the models in agreement.

When G is observed, a dependency between z and w is introduced. Interpretation of language into world state is then given by maximizing the joint probability.

# A Deepmind Paper on GLL

https://arxiv.org/pdf/1710.09867.pdf

The purpose of this paper is to clarify how exactly models with no meaningful prior knowledge learn their first words. 

- Neural nets can learn to locate referents of words and phrases in images, answer questions about visual scenes. This is called GLL. To achieve GLL, models must overcome challenges that infants face when learning their first words. While it is notable that models with no meaningful prior knowledge overcome these obstacles, researchers currently lack a clear understanding of how they do so, a problem addressed in this paper. 
- For maximum control and generality, they focus on a simple neural network-based language learning agent, trained via policy-gradient methods, which can interpret single-word instructions in a simulated 3D world. Whilst the goal is not to explicitly model infant word learning, we take inspiration form experimental paradigms in development psychology and apply some of these to the artificial agent, exploring the conditions under which established human biases and learning effects emerge. 

They define GLL as something that can learn to locate referents of words in images. A referent is just something that a linguistic expression refers to.

In this paper, they made a neural network based learning agent, that was trained via a policy gradient method, which could interpret single word instructions in a simulated 3D world.

**Experiments** - conducted in a highly controlled environment : a simulated 3D world with a limited set of objects and properties, and symbolic linguistic stimuli. In each experimental episode, the agent is presented with a single word and two objects in a room. It must move by choosing between eight motor actions, viewing the objects from different perspectives until it can determine which one best reflects the meaning of the word. It receives a single scalar positive reward if it selects the correct object by moving towards and bumping into it. The episode ends after the agent bumps into any object, or when a limit of 100 time steps is reached. To solve tasks and receive rewards, the agent must therefore first learn to perceive this environment, actively controlling what it sees via movement of its head (turning actions), and to navigate its surroundings via meaningful sequences of fine-grained actions.

They show how it exhibits various aspects of early word learning - 

- First, the agent success- fully learns a vocabulary of words from different semantic classes, and study the dynamics of this process. They show that the rate at which the agent acquires new words increases rapidly after an initial slow period, an effect matching the human vocabulary spurt (Plunkett et al., 1992; Regier, 1996). 
- Second, they investigate whether the agent exhibits a shape or colour bias. And finally, in order to analyse the semantic processing taking place in the model, they develop a novel method for dynamically visualising how different word types stimulate activations in different parts of the agent architecture.

### A 3D world for language learning

The experiments take place in the DeepMind Lab simulated world (Beattie et al., 2016). During each episode, the agent receives a single word instruction, and is rewarded for satisfying the instruction, in this case by executing actions that allow it to locate a (3D, rotating) pencil and bump into it. At each time step in the episode, the agent receives a 3 x 84 x 84 (RGB) pixel tensor of real values visual input, and a single word representing the instruction, and must execute a movement action from a set of 8 actions.

The episode ends after the agent bumps into any object, or when a limit of 100 time steps is reached. To solve tasks and receive rewards, the agent must therefore first learn to perceive this environment, actively controlling what it sees via movement of its head (turning actions), and to navigate its surroundings via meaningful sequences of fine-grained actions.

### A situated word-learning agent

The agent, combines standard modules for processing symbolic input (an embedding layer) and visual input (a convolutional network). At each time step t, the visual input v_t is encoded by the convolutional vision module and a language module embeds the instruction word l_t. A mixing module determines how these signals are combined before they are passed to an LSTM core memory. In this work, the mixing module is simply a feedforward linear layer operating on the concatenation of the output from the vision and language modules, and the language module is a simple embedding lookup (since the instruction consists of one word). 

The hidden state s_t of the core memory (LSTM) is fed to an action predictor (a fully-connected layer plus softmax), which computes the policy, a probability distribution over possible motor actions π(at|st), and a state-value function estimator Val(s_t), which computes a scalar estimate of the agent state-value function (the expected discounted future return). This value estimate is used to compute a baseline for the return in the asynchronous advantage actor critic (A3C) policy-gradient algorithm, which determines wieght updates in the network in conjunction with the RMSProp optimizer (Tieleman and Hinton, 2012). 

For an instantiation of an overall A3C agent, 16 CPU cores each instantiate a single agent and a copy of the environment, applying gradient updates asynchronously to a centralized set of weights (which the agents share). Hyperparameters for the 16 instantiations are sampled from the ranges specified later and we report the performance of the best 5 of these replicas. 

### Word learning dynamics

In our first simulation, we randomly initialized all of the weights in the agent network, and then trained it on episodes with instruction words referring to the shape, color, pattern, relative shade or position of objects. Each episode began with the agent at one end of a small room and two objects at the other. Single instruction words were presented as discrete symbols at all timesteps. The instruction word in each episode unambiguously specified one of the two target objects, but other unimportant aspects of the environment could vary maximally. Thus, shape-word instructions could refer to objects of any color-words to objects of any shape, and so on. To eliminate ambiguity, when shade words dark, light were presented, both objects differed in shade but not color, so that the meaning of the share words was comparative (as in darker, lighter). The agent received a reward of +10 if it bumped into the correct object, -10 if bumped into wrong, and 0 if the maximum number of timesteps was reached.

Findings - The agent slowly learned to respond correctly to the words it was presented with, but at some point the rate of word learning accelerated rapidly. This effect is observed in both young infant learners and connectionist simulations of word learning. By the end of successful training, the agent was able to walk directly up to the two objects and reliably identify the appropriate referent. 

Why Delay Initially - The delay in the onset of word learning can be explained by the need to acquire relatively language-agnostic capacities such as useful sequences of motor actions or the distinction between objects and walls. 

Some acceleration seems also to derive from the accusing semantic knowledge. To demonstrate this, we compared word learning speeds in an agent with prior knowledge of two words to an agent with knowledge of 20 words. The prior knowledge in this case was provided by training the agent on the word-learning task, as described above, but restricting the vocabulary to two and 20 words. So in both cases the agent has leaned to “see”and move, but the agent pre-trained on 20 words learned new words quickly. This effect accords with accounts of human development that emphasise how learning becomes easier the more the language learner knows. 

This effect accords with the idea that early exposure to simple, clear linguistic input helps child language acquisition. It also aligns with curriculum learning effects observed when training neural networks on text-based language data.

### Word learning biases

It is agreed that children exploit certain labelling biases during early word learning, which serve to constrain the possible referents of novel, ambiguous lexical stimuli. A particularly well-studied learning constraint is the shape bias whereby infants tend to presume that novel words refer to the shape of an unfamiliar object rather than, for instance, its color, size or texture. 

Example - When you’re told to imagine a car, you are equally likely to imagine it a a certain set of colors, its not like you’ll always imagine a red car, or a blue car; but rather different colors occasionally. This means that the word “car” is more associated with a shape rather than a color. But at the same time if I tell you to imagine snow for example, you will most likely see a white substance without any specific shape. 

During training, the agent learns word meanings in a room containing two objects, one that matches the instruction word and one that does not. Using this method, the agent is taught that meaning of a set C of color terms, S of shape terms and A of ambiguous terms. The target referent for a shape term can be of any color and similarly, the target referent when learning the colors in C can be of any shape. In contrast, the ambiguous terms in A always correspond to objects with a specific color and shape. 

As the agent learns, we periodically measure its bias by means of test episodes for which no learning takes place. In a test episode, the agent receives an instruction a (ambiguous) and must decide between two objects o1 and o2 not belonging to the original set. As with the original human experiment, the degree of shape bias in the agent can be measured, as the agent is learning, by its propensity to select o1 in preference to o2. Moreover, by varying the size of sets S and C, we can examine how different training regimes affect the bias exhibited by the agent. 

Regarding human learners. our simulations accord with accounts of the shape bias that emphasize the role of environmental factors in stimulating the development of such a bias. The fact that shape terms occur with greater frequency in typical linguistic environments, for American children at least, can be verified by analysis of the child-directed language corpus Wordbank. Our findings indicate that the prevalence of the human shape bias could be as much a product of the prevalence and functional importance of shape categories in the experience of typical infants as a reflection of the default state of their underlying perceptual and cognitive mechanisms. 

### Visualising grounding in both action and perception

One compelling aspect of early word learning in humans is infants’ ability to make sense of apparently unstructured raw perceptual stimuli. This process requires the learner to induce meaningful extensions for words, and to organize these word meanings in semantic memory. The success of this process has been explained by innate cognitive machinery delimiting conceptual domains, or at least for narrowing the space of possible referents. 

We analysed the trained agent to better under- stand how it solves the problem of cross-situational word learning in our setting. First, we visualised the space of word embeddings in an agent trained on words from the different classes detailed in Fig. 4, with experience sampled uniformly over words, not classes. 