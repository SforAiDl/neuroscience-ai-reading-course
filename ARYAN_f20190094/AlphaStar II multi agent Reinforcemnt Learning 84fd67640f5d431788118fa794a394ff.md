# AlphaStar II multi-agent Reinforcemnt Learning

## **Step 1: Supervised learning**

- It trains to imitate the best human player and learn their strategy
- It develops strategy on what order to build buildings and units.
- It also closely observes what actions were chosen at what scenarios.
- Just by this it performed better than 85% of humans.

## Step 2: Model

### **Observations**

1. The screen by which the agent sees(minimap). which goes through resnet or convolutional neural network.
2. The list of entities. their positions and their statistics.
3. opponent entities but only those which are on screen. all entities goes through a entity encoder or transformer.
4. scalar features like time. the race we are playing etc. these go through MLP or scalar encoder.
5. these all observations finally pass through deep LSTM which also take into account the previous actions taken. and this is what makes the strategy.

### **Predictions/Actions**

1. Mainly there are 2 types of predictions. how good is the current state and what to do or what actions to choose.
2. the model predicts what actions to take and when to take.
3. the actions which are to to be done on queued based on the delay they have and how important the action is.
4. Since the machine is only allowed to take 22 actions per 5 sec to be able to match humans limitations. it has to be selective.
5. it has a pointer network to point at which entity the actions should be executed upon.
6. it also has a deconvolutional network to point on the minimap where the action should take place.

![AlphaStar%20II%20multi%20agent%20Reinforcemnt%20Learning%2084fd67640f5d431788118fa794a394ff/Screenshot_(175).png](AlphaStar%20II%20multi%20agent%20Reinforcemnt%20Learning%2084fd67640f5d431788118fa794a394ff/Screenshot_(175).png)

## **Step 3: Training**

- The method which they have used is self play.
- these play with copy of themselves. and when on falls behind it copies from the other.
- ocasionally these play with their older selves to avoid any instabilities.
- when this is all going on there are specific models called exploiters which specifically plays with only the good models to find weaknesses.
- these exploiters are constantly reinitialized by human players
- there are some other agents called league exploiters. these do notplay among themselves but play with the main agent and older version of itself. it is specifically designed to exploit weakness of entire league.

![AlphaStar%20II%20multi%20agent%20Reinforcemnt%20Learning%2084fd67640f5d431788118fa794a394ff/Screenshot_(177).png](AlphaStar%20II%20multi%20agent%20Reinforcemnt%20Learning%2084fd67640f5d431788118fa794a394ff/Screenshot_(177).png)