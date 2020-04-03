- Continuous Action Spaces, we use the quatntiy of the Q values as well. Hence we do not use Softmax since the value of the prediction is used.
#### Actor
- Actor runs randomly to fill the expereince replay.
- The actor predicts the Q values for all actions and Critic predicts the Maximum Q value. We train the model to predict same values for both, Indirectly.

#### Critic
- The Crtic trains the Actor
- Critic uses historical data, it has access to all future states. The nextObs is used to calculate Q value
- It aims to maximize Q value. The Actor is trained to predict action for which Critic predicts maximum Q value.
- The Critic is greedy


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
