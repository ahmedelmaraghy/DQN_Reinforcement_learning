# DQN : Deep Q-Networks:
This is a solution for the unity based banana-collector game as part of Udacity's Nano degree program.

## Environment:
The agent is in a large square world (fenced). There are yellow and blue bananas scattered in the environment. The agent's goal is to avoid collecting blue bananas and collect as much yellow bananas as possible. In each time step the agent (player) can take an action to move either forward, baclward, turn left, or turn right.
### State and Action Space:
The state space has 37 dimensions and contains the agent's velocity, along with ray-based perception of objects around agent's forward direction. Given this information, the agent has to learn how to best select actions.  Four discrete actions are available, corresponding to:
- **`0`** - move forward.
- **`1`** - move backward.
- **`2`** - turn left.
- **`3`** - turn right.

## The Reward Function:<br/>
In order to maximize the number of yellow bananas and penalize the collection of blue bananas, the agent is given a reward of +1 for collecting a yellow banana and -1 for collecting a blue banana. The task is episodic, and in order to solve the environment, the agent must get an average score of +13 over 100 consecutive episodes. 

The reward function is, however, not focusing on a time limit for reaching the target. 
(Otherise, a slight -ve reward could be given on time steps, in order to finish the episode as fast as possible)

## Solution:
The DQN (Deep Q-Network) algorithm was used to train the agent to solve the environment.

The solution is divided into 3 files:
- **Model.py** : Conatins the functions related to the neural network structure (later on, 2 instances of the function will be used in dqn_agent.py)
- **dqn_agent.py**: Contains the functions defining the agent's DQN algorithm.
- **Navigation.ipynb**: Contains the reaclling of the funtions to solve the environment.

### Brief Explanation:<br/>
The vaue-based algorithm relies in its core on a neural network that takes as an input the state value (or image frames in pixels) and then using the NN, that is initialized first to random weights, produces action values for the 4 actions acailable each time step.

Based on Epsilon-greedy algorithm, the agent takes an action. If the probability is greater than epsilon, the action with highest action value is taken. Otherwise, the action is randomly taken among the 4 actions.

**So how does the agent learn?**<br/>
By dreaming again about its experience ! 
Each time step the agent saves a snapchot feedback of what happended to it (state, action, reward, new state).
Once it has enough *experience* to sample from, the agent starts to *learn* from them. 
To make the cost function stable, the target value (reward + the action value of the next state) is retrieved from a non-trained neural network in which its weights are initialized by the same weights of the network to be trained. 
Then, after each batch of training (using Stochastic gradient descent), the wights of the *trained neural network* is then copied to the * untrained (or target)* neural network. The learning continues with the aim of maximizing the expected reward.

### Output:
The environment is solved in 382 episodes <br/>	
Average Score: 13.03 <br/>




