# Collaboration and Competition 

## Introduction

FTo solve the environment in this project, I've decided to implement the MADDPG algorithm. MADDG is a great choice for this environment due to the existence of multiple agents.


## Learning Algorithm

The [MAPPDG algorithm](https://arxiv.org/pdf/1706.02275.pdf) was introduced as an extension of DDPG for multi-agent environments. One simple way to think of MADDPG is as a wrapper for handling multiple DDPG agents. But the power of this algorithm is that it adopts a framework of centralized training and decentralized execution. This means that there is extra information used during training that is not used during testing. More specifically, the training process makes use of both actors and critics, just like DDPG. The difference is that the input to each agent's critic consists of all the observations and actions for all the agents combined. However, since only the actor is present during testing, that extra information used during training effectively goes away. This framework makes MADDPG flexible enough to handle competitive, collaborative, and mixed environments.


In MADDPG, each agent has its own actor local, actor target, critic local and critic target networks. The model architecture for MADDPG resembles DDPG very closely. The key difference is however, the Critic Network takes both of the states and concatenates them and uses them to calculate the Q values and further improve the actor. DDPG, on the other hand, concatenates the actions to the input of the second hidden layer, after the states have already gone through in the first hidden layer. This was new to me, I did not know that for the critic, I had to combine the state and action for both of the agents.

## Training and Results

![Training Results](https://github.com/abheesht17/TennisAgent/blob/master/Media/training.PNG)

I found training to be particularly challenging for my final MADDPG implementation. Initially, I had many issues getting the full implementation to work as expected. Even after the issues were fixed, the training was very unstable. A lot of hit and trail went into making the algorithm stable:

![MADDPG Plot of Rewards](https://github.com/abheesht/TennisAgent/blob/master/Media/plot.PNG)

The results above show that the training process followed a stable pattern, and the 100-episode rolling max score never went significantly down after solving the environment.

Here are the final values for the hyperparameters I ended up using:

```
BUFFER_SIZE = 100000
BATCH_SIZE = 256
GAMMA = 0.99
TAU = 1e-3
LR_ACTOR = 1e-4
LR_CRITIC = 1e-3
WEIGHT_DECAY = 0.0
```
## Future Work Ideas

I would like to run parallel instances of MADDPG agents to get quicker results. 

I would like to grid search the hyperparameters for a truly optimal model that might be able to get a score higher than 0.5, consistently.

