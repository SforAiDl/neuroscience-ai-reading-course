# Intrinsic social motivation

## NEED OF IMPROVEMENT

- In previous methods the environment had hand-crafted reward system which not natural
- or it allowed the agents to view rewards of the other agents.
- and some were using centralized training for getting coordination among the agents.
- with all this communication between the agents still remains a challenge.

## BASIC IDEA

- So basically the agent is rewarded if it has some influence on the other agent and this is calculated by getting the difference between the predicted behavior of the other agent without the agent and the actual behavior due to the influence of the agent.

## MOA

- MOA or model of other agents is what used to predict actions of other agents.
- the agent then behaves in such way to has different outcome than predicted. thus the difference in the actions is used as a basis of reward system.
- so the net reward looks something like this,

![Intrinsic%20social%20motivation%202bf0fc2ab0804eb3a51408d8eb12403c/Screenshot_(189).png](Intrinsic%20social%20motivation%202bf0fc2ab0804eb3a51408d8eb12403c/Screenshot_(189).png)

- in this method we centralized training to compute c^k. and also one the agent who is being influenced will not have influential reward system construct. these problems will be dealt with later.

## COMPARISON

- the following shows the comparison between the model with actor-critic and with a similar model with no reward given on influence and also change their actions prediction the actions of the other agents.

## CLEANUP  GAME

![Intrinsic%20social%20motivation%202bf0fc2ab0804eb3a51408d8eb12403c/Screenshot_(188).png](Intrinsic%20social%20motivation%202bf0fc2ab0804eb3a51408d8eb12403c/Screenshot_(188).png)

- the single purple agent was trained with social influence reward. unlike the other agents which continue to explore until an apple is found.
- the influencer only traverses through the map when it is pursuing an [apple.so](http://apple.so) the influencee(yellow agent) notices this behaviour and by observation knows that there must be an apple outside its bounds if the purple agent moves.
- but this system can also lead to negative influence.

## COMMUNICATION CHANNEL

- at each time step each agent send s a random discrete symbol tMk so it is combined to form a message vector.

![Intrinsic%20social%20motivation%202bf0fc2ab0804eb3a51408d8eb12403c/Screenshot_(186).png](Intrinsic%20social%20motivation%202bf0fc2ab0804eb3a51408d8eb12403c/Screenshot_(186).png)

- the visuals and the message vector is put through the lstm which gives separate policy for the actions and the message.
- so the same method is used to determine how much the agent had an influence on others.
- so this solves the problem mentioned previously of having negative influence .

                     

## IMPROVED MOA

![Intrinsic%20social%20motivation%202bf0fc2ab0804eb3a51408d8eb12403c/Screenshot_(187).png](Intrinsic%20social%20motivation%202bf0fc2ab0804eb3a51408d8eb12403c/Screenshot_(187).png)

- So instead of accessing the model of the other agents, we can add another fully connected lstm to predict their behavior.th
- this MOA can be used to "imagine " other actions it could have taken and calculate which action has the most influence on the other agent.