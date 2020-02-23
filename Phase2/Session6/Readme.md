## Reinforcement Learning:

Code: http://ai.berkeley.edu/reinforcement.html

1. \_\_init\_\_
   This function creates an MDP and returns the policy. The policy is created by calculating the values iteratively.
   - Initialise the discount.
   - Initialise the Number of iterations run to get a policy
   - Initialise the values to a Counter(dictionary)
   
   - Initialise the states
   - Initilialise the probabilities for each next state
   - For each number if Iterations:
         -- Copy values
         For each state:
            -- Initialize Final Value to None
            for each action in possible Actions:
               -- currentValue is computeQValueFromValues from current state, current action
   
2. getQValue
3. computeValueFromQValue
4. computeActionFromQValues
5. getAction
6. update
