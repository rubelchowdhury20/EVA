### Explanation of code for T3D network

#### Step 1:

For training the network we don't use sequential data here, cause it's possible that it might learn only from the consecutive steps. So, overcome this issue we use the concept named **Replay Buffer**.

In this process, we have one buffer memory, where we store the transaction parameters in tuple format viz (**S** -- current state, **A** --current action, **S'** -- next state, **A'** -- next action).

The buffer is filled with these tuples till the maximum size and while training one example is randomly sampled for training the network.



#### Step 2:

In T3D we have two Actors named **Actor Model** and **Actor Target**.

The Actor Model takes the state as input and returns the prediction actions.

The Actor Model is trained using back-propagation, while the Actor Target is trained using polyak average.

The amplitude of the actions are decided by the max-action parameter.



#### Step 3:

The T3D has total 4 Critics having two models named **Critic_1 Model** and **Critic_2 Model** while there are two targets named **Critic_1 Target** and **Critic_2 Target**.

Critic Model is trained using back-propagation and critic target is trained using polyak average.



#### Step 4:

Both the Critic Target interact with the environment and we take the minimum q value from them. We pass it to critic model and critic model in return updates the Actor Model.

The we train the Target Models using Polyak average.

This steps starts the training process by fetching train samples from the reply_buffer obj. It then loads the return values on device.
the inputs are replay_buffer obj, num_iterations to run training, batch_size, discount factor(from bellman equation), tau is for polyak averaging, policy noise value to add to actions, max value of the actions, update factor for our actor.



#### Step 5:

We use next_state and next_action to train our Critic. The next_state is passed to actor_target model to predict the next_action.



#### Step 6:

Gaussian noise is added to our next_action.



#### Step 7:

The two inputs next_state and next_action are passed to the Critic class which returns two Target Model q value prediction, target_Q1 and target_Q2



#### Step 8:

The minimum value of target_Q1 and target_Q2 is taken.



#### Step 9:

The done parameter is used to indicate if the episode is over and then we calculate final target_Q.



#### Step 10:

The current_Q  values are calculated from 2 critic model networks.



#### Step 11:

Loss is calculated using both current_Q and target_Q.



#### Step 12:

Backpropagate the loss on critic model after clearing the grads.



#### Step 13:

train the actor after training the critic twice(policy_frequncy)
actor loss is calculated by passing current state to critic and the action predicted by the actor(sort of like adverserial loss) and mean over a batch



#### Step 14:

Update Actor target by polyak Average once every two iterations.



#### Step 15:

Update the Critic Target by polyak Average once every two iterations.