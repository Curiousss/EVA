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
