- Continuous Action Spaces, we use the quatntiy of the Q values as well. Hence we do not use Softmax since the value of the prediction is used.
#### Actor
- Actor runs randomly to fill the expereince replay.
- The actor predicts the Q values for all actions and Critic predicts the Maximum Q value. We train the model to predict same values for both.
- Actor model is updated using backpropagation, like a short term memory of events.
- Actor Target is updated using Polyak Avg, using the partial weights of Actor model. Long term Memory 

#### Critic
- The Crtic trains the Actor
- Critic uses historical data, it has access to all future states. The nextObs is used to calculate Q value
- It aims to maximize Q value. The Actor is trained to predict action for which Critic predicts maximum Q value.
- The Critic is greedy

#### Model


#### Target


#### Flow
- The Actor Model takes next state(which has not yet happened).
