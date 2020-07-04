# HIDE AND SEEK

![HIDE%20AND%20SEEK%2010067df7e23b4b2e8fba1663f0c5b91e/Screenshot_(179).png](HIDE%20AND%20SEEK%2010067df7e23b4b2e8fba1663f0c5b91e/Screenshot_(179).png)

## NEED FOR IMPROVEMENT IN SINGLE AGENT RL

- collecting demonstrations and specifying reward functions can be costly and time consuming
- once the rl has found a way to perform a particular task it has no scope of improvement.
- all the other ways like unsupervised exploration scale poorly on complex environment.

## BEFORE ACTUAL TRAINING

- the agents were trained in a number of other tasks like object permanence, navigation and construction. and it showed much better results in an actual game of hide and seek.

## REWARD SYSTEM

- it is a team based reward system
- +1 for the hiders and -1 for the seekers if all the hiders are hidden
- -1 for the hiders and +1 for the seekers if any one is spotted
- and -10 if any of them go outside arena.
- episode lasts 240 timesteps and first 40% are for preptime.

![HIDE%20AND%20SEEK%2010067df7e23b4b2e8fba1663f0c5b91e/Screenshot_(180).png](HIDE%20AND%20SEEK%2010067df7e23b4b2e8fba1663f0c5b91e/Screenshot_(180).png)

## POLICY OPTIMISATION

- this uses two networks- policy network that produces action distribution and other a critic network which predicts discounted future rewards.
- policy optimisation is done using proximal policy optimisation.
- it utilises decentralised execution and centralised training.
- that is similar agents have different brains but they share the same weights

## OBSERVATIONS

- we notice that there was no direct incentives to use ramps and develop strategies it was solely due to adaptability on the changing environment.
- hiders learn efficient division of labor for instance while constructing a shelter the agents would bring their own separate box.
- these agents were used on multiple other tasks which required cognition/remembering skills and construction tasks. surprisingly the agents which were pretrained in hide and seek performed better than who trained from scratch.

## COMPARISON WITH INTRINSIC MOTIVAITON

- intrinsic motivation is heavily based on exploration. but sometimes explorations can be 'noisy' i.e unuseful.
- when intrinsic motivation applied to the system the number of box usage seems to be higher than self-play but when the number of boxes and players increase agent and in particular box movement decreased.
- this proves that when the environment scales the methods like count based because the things that are interesting or needed to be explored more are to be hand specified.

## 

![HIDE%20AND%20SEEK%2010067df7e23b4b2e8fba1663f0c5b91e/Screenshot_(181).png](HIDE%20AND%20SEEK%2010067df7e23b4b2e8fba1663f0c5b91e/Screenshot_(181).png)