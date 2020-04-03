- Continuous Action Spaces, we use the quatntiy of the Q values as well. Hence we do not use Softmax since the value of the prediction is used.
#### Actor
- Actor runs randomly to fill the expereince replay.
- Many Actors are running Asynchronously to fill the replay buffer.
- The actor predicts the Q values for all actions and Critic predicts the Maximum Q value. We train the model to predict same values for both, Indirectly.

#### Critic
- The Crtic trains the Actor
- Critic uses historical data, it has access to all future states. The nextObs is used to calculate Q value
- It aims to maximize Q value. The Actor is trained to predict action for which Critic predicts maximum Q value.
- The Critic is greedy we have 2 Critics(There can be more than 2 critics theoritically.). Ee pick minimum of the maximum Qvalues predicted by Critic1 and Critic2. The Critic is being conservative. 
- Both Critic 1 and 2 are updated equally.
- The Critic Target is the final model that will be used


#### Model
- Trained using backpropagation, like a short term memory of events.

#### Target
- Trained by updating using Polyak Avg, using the partial weights of model, like long term Memory 
- Delayed update, hence stabilized


#### Flow
- 2 similar DNNS for Actor Model and Target
- 4 similar DNNs are created for Critic 1 Model and Target, and Critic 2 Model and Target.
- Critic is run and updated twice before updating the model.
- The Actor Model takes next state(which has not yet happened).

- Critics Model 1 and 2 are run twice and back propagated
- Then Actor Model is back propagated
- Then the Target Actor, Critic 1 and 2 are updated using Polyak Averaging

- 100000 episodes and 100 batch size, each episode is (s, s', a, r)
- s' is the next observation that is not seen yet, and the AT is guessing the action a'
- s'-> AT-> a' x gaussian noise 
- Gaussian noise is used because we are trying to predicted for a next unseen observation. The noise also adds stochasticity. Since it gives a range of possible values it gives stability to the Critic.
- (s', a') -> CT1 - > Qt1(s', a')
- (s', a') -> CT2 - > Qt2(s', a')
- Q_final_Target = R x gamma x minimum(Qt1, Qt2)

- s is the current observation 
- (s, a) -> CM1 -> Qm1(s,a)
- (s, a) -> CM2 -> Qm2(s,a)
- Critic Loss = MSELoss (Qm1(s,a), Q_final_Target) + MSELoss (Qm2(s,a), Q_final_Target)
- Backprop the Critic Loss to CM1 and CM2

- s -> AM -> a
- (s, a) -> CT1 - > Qt1(s', a')
- (s', a') -> CT2 - > Qt2(s', a')
- > Actor Loss = Maximize V values
- Backpropagate on AM

- After repeating all the above steps twice update the Targets(A, C1 and C2) using Polyal Averaging (Delayed).
- W' = tau * W + (1 - tau) * W'



# CODE
  
  INITIALIZATION  We initialize the Experience Replay Memory, with a size of 20000. We will populate it with each new transition



```python
import os
import time
import random 
import numpy as np 
import matplotlib.pyplot as plt 
import pybullet envs 
import gym 
import torch 
import torch.nn as nn 
import torch.nn.functional as F 
from gym import wrappers
from torch.autograd import Variable 
from collections import deque

```

We initialize the Experience Replay Memory with a size of `max_size` 1e6.
Then we populate it with new transitions.
Allow the Agent to run randomly and fill up the Replay Buffer `addTransition`. 
We need the Replay Buffer/Memory ready before training the Critic.
We run full episodes with the first 10,000 actions played randomly, and then with actions played by the Actor Model. This is required to fill up the Replay Memory. 


The replay buffer, `storage` is an array and the `ptr` is moved from postion 0 to end as and when the trasitions are added, after reaching the end that is `max_size`, the pointer resets to 0 and the new transitions are over-written and this continues.

`sample` samples a `batch_size` of data randomly from the `storage` replay buffer. the length of `storage` maybe less than or equal to `max_size` while `storage` replay buffer is still getting updated.
`batch_dones` is a `done` switch for each batch to check if the episode is done completely or not.

Make any array each for `batch_states, batch_next_states, batch_actions, batch_rewards, batch_dones`from element of the tuple (`state, next_state, action, reward, done`) which the tranistion from each entry in the `storage`. There will no duplicate copies of these entries but multiple references to the memory location is used. Now return these new arrays.


```python
class ReplayBuffer(object):
  # Init is there for all classes to initialize an object
  # Self is pointer to the object of the class which is initialized
  def __init_(self, max_size = 1e6):
    self.storage =[] 
    self.max_size = max_size 
    self.ptr = 0

def add(self, transition):
  if len(self.storage) == self.max_size:
    self.storage[int(self.ptr)] = transition 
    self.ptr = (self.ptr + 1) % self.max_size
  else:
    self.storage.append(transition)

def sample(self, batch_size):
  ind = np.random.randint (e, len(self.storage), batch_size) 
  batch_states, batch_next_states, batch_actions, batch_rewards, batch_dones = [], [], [], [], [] 
  
  for i in ind:
    state, next_state, action, reward, done = self.storage[i] 
    batch_states.append(np.array(state, copy = False)) 
    batch_next_states.append(np.array(next_state, copy = False)) 
    batch_actions.append(np.array(action, copy - False)) 
    batch_rewards.append(np.array(reward, copy - False)) 
    batch_dones.append(np.array(done, copy - False) 
  return np. array (batch_states), np.array(batch_next_states), np.array(batch_actions), np.array(batch_rewards).reshape(-1, 1), \
          np.array(batch_dones).reshape(-1, 1)
```

We build TWO kinds of actor models. One called the Actor Model and another called the Actor Target.

Build one DNN is defined to be used for both the Actor model and the Actor Target.
The Actor Model is trained using Back Propagation while training on Experience Replay buffer.
The Actor Target is trained using the updates from Actor Model through Polyak Averaging, stabilization algorithm. Using Polyak averaging, our targets are not as reactive to changes as models. Targets are delayed in their training as well, which means we allow our models to stabilize first before we update targets. 

So they get similar to the model only if the model is consistent.   
Actor Model and Actor Target models have exactly the same DNN definitions.



`state_dims` is the state parameters defining the number of variables in a state. These variables define the state in the environment. Eg. Where is the arm of the  robot

`action_dim` is the number parameters to define the actions that can be taken. Value of each action (eg. Right Left) is a floating point number representing the quantity of a particular action(Eg. 5 degree to the left).

`max_action` is the limit of this quantity of an action (Eg. 90 degrees)

The `forward` function outputs `x` the actions, which is scaled to -1 to 1 using tanh activation and multipled by `max_action` to get the exact quantity of each action.


```python
class Actor (nn. Module):
  def __init__(self, state_dims, action_dim, max_action):
    #Max action is to clip in case we added too much noise
    super(Actor, self).__init__# activate the inheritance 
    self.layer_1 = nn.Linear(state_dims, 400) 
    self.layer_2 = nn.Linear(400, 300) 
    self.layer_3 = nn.Linear(300, action_dim) 
    self.max_action = max_action

def forward(self,x):
  x = F.relu(self.layer_1(x)) 
  x = F.relu(self.layer_2(x)) 
  x = self.max_action * torch.tanh(self.layer_3(x))
  return x
```

STEP 3 We define 1 DNN for Critic 1 and 2. 
Critic 1 and 2 are just different set of layers in a neural network. `Forward` function returns 2 outputs from 2 different layers from critic 1 and 2. 
We Build 2 DNNs, for the two Critic models and two for the two Critic Targets

We do not have `max_action` in Critic since action is coming from Actor DNN where it is taken care.

Critic takes state `x` and action `u` and concatenates it(vertically) before sending it to the DNN layers

The Q1 function is a separate forward function that does not back propagate. It is used to train the Actor using the layers of Critic 1. It does not matter whether critic 1 or 2 is used here in the long run.



```python
class Critic(nn.Module):
  def __init__(self, state_dims, action_dim):
    #max_action is to clip in case we need added too much noise
    super(Critic, sell).__init__() #activate the inheritence
    #First Critic Network
    self.layer_1 = nn.Linear(state_dims + action_dim, 400) 
    self.layer_2 = nn.Linear(400, 300) 
    self.layer_3 = nn.Linear (300, action_dim) 
    #Second Critic Network 
    self.layer_4 = nn.Linear(state_dims + action_dim, 400) 
    self.layer_5 = nn.Linear(400, 300) 
    self.layer_6 = nn.Linear(300, action_dim)

def forward(self, x, u): 
  # x is state, u is action 
  xu = torch.cat([x, u], 1) # 1 for vertical concatenation, 0 for Horizontal
  #forward propagation on first Critic
  x1 = F.relu(self.layer_1(xu)) 
  x1 = F.relu(self.layer_2(x1)) 
  x1 = self.layer_3(x1) 
  # forward propagation on second Critic 
  x2 = F.relu(self.layer_4(xu)) 
  x2 = F.relu(self.layer_5(x2))
  x2 = self.layer_6(x2)
  return x1, x2

def Q1(self, x, u): 
  #x state, u- action This is used for updating the Q values 
  xu = torch.cat([x, u], 1) # 1 for vertical concatenation, 0 for horizontal
  x1 = F.relu(self.layer_1(xu))
  x1 = F.relu(self.layer_2(x1)
  x1 = self.layer_3(x1)
  return x1
```

Training process. Create a T3D class, initialize variables and get ready for step 4

The `actor` is the Actor Model that is trained using the backpropagation.
The `actor` and `actor_target` are initialized using `state_dims, action_dim, max_action`, same as explained earlier.

The weights of the `actor_target` is initialized to the weight of the `actor`. This is updated using Polyak Averaging.

Similarly...

The `critic` is the Critic Model that is trained using the backpropagation.
The `critic` and `critic_target` are initialized using `state_dims, action_dim`, same as explained earlier.

The weights of the `critic_target` is initialized to the weight of the `critic`. This is updated using Polyak Averaging. 

`select_action` takes the current state(converted to tensor) calls the Actor Model(forward function) to get the action(converted to numpy).The output action that is sent to the Critic forward function `Q1` explained earlier. 



```python
# Select CPU or GPU
device = torch.device('cuda' if torch.cuda.is avallable() else cpu)

# Building the whole Training Process into a class
class T3D(object):
  def __init__(self, state_dims, action_dim, max_action):
    # making sure out T3D can work with any environment
    self.actor = Actor(state_dims, action_dim, max_action).to(device) #GD
    self.actor_target = Actor(state_dims, action_dim, max_action).to(device) #Polyak Averaging
    self.actor_target.load_state_dict(self.actor.state_dict)
    #Initializing with model weights to keep them same
    self.actor_optimizer = torch.optim.Adam(self.actor parameters()
    
    self.critic = Critic(state_dims, action_dim).to(device) #GD 
    self.critic_target = critic(state_dims, action_dim).to(device) #Polyak Averaging 
    self.critic_target.load_state_dict(self.critic.state_dict) 
    #Initializing with model weights to keep the same 
    self.critic_optimizer = torch.optim.Adam(self.critic.parameters()) 
    self.max_action = max_action

def select_action(self, state):
  state = torch.Tensor(state.reshape(1, -1)).to(device) 
  return self.actor(state).cpu().data.numpy().flatten() 
  # Need to convert to numpy remember clipping!

```


Sample from a batch of transitions (s, s', a, r) from the memory

* `replay_buffer` is replay buffer object defined earlier, 
* `iterations` is number of iterations of the training, 
* `batch_size`=100 number of transitions in an input batch, 
* `discount`=0.99 is the discounting factor in the bellman Equation,
* `tau` = 0.005 is a parameter for Polyak Averaging, 
* `policy_noise` = 0.2 noise added to the actions, 
* `noise_clip`=0.5 maximum quantity of the action based on the given environment, 
* `policy_freq`=2 how often the Actor is updated

For the number of `iterations` defined repeat:
* Get an array of sample of transitions from `replay_buffer` of size `batch_size`
* The sample is the set of arrays `batch_states, batch_next_states, batch_actions, batch_rewards, batch_dones` as explained earlier.
* Convert each of them to a Tensor as needed by the DNN.



```python
def train(self, replay_buffer, iterations, batch_size=100, discount=0.99, \
          tau = 0.005, policy_noise = 0.2, noise_clip=0.5, policy_freq=2):
  for it in range(iterations):
    # Step 4 We sample from a batch of transitions (s, s', a, r) from memory 
    batch_states, batch_next_states, batch_actions, batch_rewards, batch_dones = replay_buffer.sample(batch_size)
    state = torch. Tensor(batch_states).to(device) 
    next_state = torch.Tensor(batch_next_states).to(device) 
    action = torch.Tensor(batch_actions).to(device)
    reward = = torch.Tensor(batch_rewards).to(device)
    done = torch.Tensor (batch_dones).to(device)
```

Step 5: 
From the next state s\`, the Actor target plays the next action a\`. Both are used later by the Critic


```python
self.actor_target.forward(next_state)
```

We add Gaussian noise to this next action a'. This is the same as exploration!
The noise is calculated by applying `normal_` function from `Torch` on the `batch_actions` which is the array of all actions in the given sample. The mean is 0 and standard deviation is `policy_noise` which is a hyper parameter.
Then we clamp the noise to a set limit using `noise_clip` which is a hyper parameter.
After applying this noise to `next_action` the `next_action` is also clamped in a range of action values supported by the environment using `max_actions`
Step 6:


```python
noise = torch.Tensor(batch_actions).data.normal_(0, policy_noise).to(device) 
noise = noise.clamp(-noise_clip, noise_clip) 
next_action = (next_action + noise).clamp(-self.max_action, self.max_action)
```

 STEP 7 
The two Critic targets take each the couple (s', a') the `next_state` and `next_action` calculated earlier as input and return two Q values,
`target_Q1`(s', a') and `target_Q2`(s', a') as outputs





```python
target_Q1, target_Q2 = self.critic_target.forward(next_state, next_action)
```

 STEP 8 Keep the minimum of these two Q-Values. his is not target_Q, we are just being lazy, and want to use the same variable name later on. 

It represents the approximated values of the next state.
Taking a minimum of the 2 Q-values prevents too optimistic estimates of that value of the state!

In classic Actor-Critic Method (with 1 Critic) we had overly optimistic estimates which prevented the training process from being stable, and taking the minimum of 2 Q-Values here adds that stability which was required. 


```python
target_Q = torch.min(target_Q1, target_Q2)
```

 STEP 9 
We get the final target of the two Critic models, which is:

Qt = `reward` + `discount`  * `Qt`

`discount` is gamma

`Qt = min(Qt1, Qt2)`

BUT... We are run this only if the episode is not over that is `Done = 0` which is integrated in the above equation with `(1-done)`.

We use Pytorch detach to copy the value or make a branch to avoid target_Q to create it's computation graph hence avoid backprop on itself.


```python
target_Q = reward + ((1-done) * discount * target_Q).detach()
```

 STEP 10 
Two critic models take (s, a) the current state and current action and return two Q-Values respectively.


```python
current_Q1, current_Q2 = self.critic.forward(state, action)
```

 STEP 11 
 
 We compute the loss coming from the two Critic models: 


```python
critic_loss = Mse_loss(current_Q1, target_Q) + F.mse_loss(current_Q2, target_Q)
```

 STEP 12 
Backpropagate this critic loss and update the parameters of two
Critic models with Adam Optimizer


```python
selt.critic_optimizer.zero_grad() #Initialize the gradients to zero
critic_loss.backward() #Computing the gradients
self.critic_optimizer.step() #Performing the weight updates
```

 STEP 13 
Once every two iterations defined by `policy_freq`, we update our Actor model by performing gradient ASCENT on the output of the first Critic model. 
* First call Actor Model with Current state to get current action.
* Call the Q1 forward funtion of Critic(that does not backprop on Critic) send Current state and current actionusing to get the Q value.
* Take a mean of that Q value (of all the Asynchonous Actors of a batch)
* Take the negative of the mean to perform gradient ascent and Backprop.


```python
if it % policy_freq == 0:
  #This is DPG part 
  actor_loss = -(self.critic.Q1(state, self.actor(state)).mean())
  self.actor_optimizer.grad_zero() 
  actor_loss.backward() 
  self.actor_optimizer.step()
```

 STEP 14 
By now the Critics are updated 4 times.

Once in every two iterations, we update our Actor Target by Polyak Averaging.

The parameters in Actor Model and Actor Target are defined from same Actor class so each parameter can be paired respectively and iteratied using `zip` and `for` loop.

* For each parameter in Actor Model `param` and Actor Target `target_param`, update parameters of Actor Target directly using the respective parameter of the Actor Model using the  Polyak Averaging Equation:

* target_param.data.copy_(tau * param.data + (1 - tau) * target_param.data) 

Using the data part of the parameter Tensors.

Where tau 

Now, why do we have Different Actor Target and Actor Models? 
Well, they can be the same, and in fact, in many naive RL models, they are the same. 
But we can improve overall performance by keeping two models and updating them from each other. 
Once every two iterations, we update the weights of the Actor target by Polyak averaging


```python
for param, target_param in zip(self.actor.parameters (), self.actor_target.parameters()):
  target_param.data.copy_(tau * param.data + (1 - tau) * target_param.data) 
```

This way our target comes closer to the model. 

 STEP 15 
In once every two iterations, we update our Critic Target by Polyak Averaging
Similar to the way the Actor Target is updated as explained in the previous step.

Where is the DELAYED part of the T3D?
We update our models at every step, but our target once every two steps. 


```python
for param, target_param in zip(self.critical.parameters(), self.critic_target.parameters()):
  target_param.data.copy_(tau * param.data + (1 - tau) * target_param.data)

```
