## 1: backprop

1. Why is normalization of inputs a recommended heuristic?
2. In the ADAM momentum model explain the effect of the (corrected) variance.

3. Also in ADAM, what is the $\epsilon$ parameter used for?

## 2: Consider deep learning models

1. Explain why dropout works as a regularization technique

Regularization is a technique used in machine learning and statistics to prevent overfitting by adding a penalty term to the loss function. Overfitting occurs when a model learns the training data too well, capturing noise in addition to the underlying patterns.

Dropout is the process by which we don't take into account the output of certain randomly selected neurons during forwards propagation, this is done by zeroing the output of the neurons in question.

This works as a means of normalization given we can zero the values of the dropped nodes, and normalize the values of the retained nodes with the probability of the selection we used in the random select.

The consequence of this action is to de-bias the network, this is done by making the network less dependant on certain nodes given they can be dropped out and by consequence requiring the remaining set to make appropriate decisions.

This is further verified by the addition of noise to the network, and the network still being able to give appropriate results.

1. Why have CNN virtually replaced MLP in machine learning

CNN or Convolutional Neural Networks are a type of MLP which use convolution in place of general matrix multiplication in at least one of their layers.

There are 3 main reasons why CNN have replaced MLP's 
- This types of networks are very efficient in 2D environment and at detecting patterns in these types of environments, this being said it is simple to see one of their main purposes is for image analysis
- Given they are able to take advantage of the general structure of the data, this type of network also is characterized by requiring less parameters that their non convolutional counterpart, this permits not only less parameters to optimize but less feature space to consider all leading to higher efficiency.
- In consequence of smaller amount of parameters and higher proclivity for 2D spaces, this network type also benefits a lot from being run in GPU's over CPU's this not only leads to better efficiency but also allows for better parallelization of the computation.


1. In a GAN the stopping condition is observed by checking the generator or the discriminator ? in particular what is observed

A Generative Adversarial Network (GAN) consists of two main components: a generator and a discriminator. The generator's job is to produce fake data to pass to the discriminator. The discriminator, on the other hand, has the task of determining whether the data it receives is real (from the true dataset) or fake (from the generator).

In GAN the stopping condition can be seen in the discriminator can be seen in 2 factors:
- generator samples are indistinguishable from real data 
- discriminator is correct $\frac{1}{2}$ of the time

Usually the factor we are looking is the discriminators accuracy given it is simpler to analyze than to detect the error rate of the generators samples.


1. Why are vanishing and exploding gradients characteristic of deep models in temporal processing?

Vanishing and exploding gradients are common issues encountered when training deep learning models, particularly those dealing with sequential or temporal data, such as Recurrent Neural Networks (RNNs) and Long Short-Term Memory (LSTMs).

Vanishing and exploding gradients occur when there are several multiplications from the output layers towards the input layer, these multiple multiplications by the weights (which are usually values which are less or grater than 1), lead to either the values getting infinitesimally small or infinitesimally large, leading to unusable values for the weights.

These values are more significant in temporal processing given we are working with long-range dependencies over multiple time-steps, and given each time-step corresponds with a multiplication the proclivity for this type of problem is greater.

2. What is the main difference between LSTM and recurrent (RNN) neural networks ? Explain why the difference provides a clear advantage to one of those models.

LSTM's are a type of RNN defined as a gated RNN.

LSTM's ocurred as consequence of learning long term dependencies in RNN's (problems such as vanishing and exploding gradients).

The main difference, and the way to solve this problem with long term dependencies, was the introduction of memory cells in the LSTM in place of normal nodes in the RNN.

Each of these memory cells contains an internal state, i.e., a node with a self-connected recurrent
edge of fixed weight 1, which ensures that the gradient can pass across many time steps without
vanishing or exploding.

This gives a clear advantage to LSTM given that RNN require more complex solutions to be able to learn these long term dependencies such as Gradient clipping.

## 3: Consider Reinforcement Learning (RL)

1. Why is RL not adequate to a strict classification problem?

Reinforcement learning is a type of learning in which an agent interacts with an environment and gets a reward depending on the interaction, his intention will be to maximize the reward, the goal will be for the agent to learn from the action rather than being taught directly.

In contrast a classification problem, is a type of problem where out goal will be to classify inputs into discrete classes, with this in mind this type of problem are usually classified as supervised learning and therefore are trained on labelled data.

RL is therefore not adequate for a classification problem given we don't have previously labeled data nor discrete classes into which to classify our input.

2. Suppose that $\gamma = 0.5$ and the agent receives rewards $R_1 = -1, R_2=-1, R_3=1, R_4=3, R_5=2$, with $N=5$. What are the values of $G_0, G_1,...,G_5$?
3. Why is policy convergence typically much faster than value convergence?

Policy convergence is generally faster than value convergence given better actions are faster to find than their exact values.

This happens because the problem related with categorizing an action better or worst according to a policy is usually simpler than the calculation of a value for all state-action pairs, which can be n-dimensional and therefore multiple times more complex.

1. In the $\epsilon$-greedy model why can't the value of $\epsilon$ be small from the start?


In $\epsilon$-greedy models, $\epsilon$ is a variable related with exploration (idk name), its purpose is to define a policy because it where the agent chooses the optimal action (under the current estimate Q) with probability 1 - $\epsilon$ but explores randomly with the remainder probability $\epsilon$.

With this in mind, if we have a small value of epsilon to start then the initial moves of the agent will have high probability of choosing the best action in the current state, given the agent doesn't have a clear concept of what a good action is given it just started training, these moves will be analogous to choosing randomly.

The optimal way to use $\epsilon$ is to start with a higher value and decrease it over time, trying to maximize speed and accuracy.

## 4: a medley...

1. Can a CNN with a softmax output be seen as a dynamical structure mixture model?

Dynamic Structure mixture model, is the application of dynamic structure to a set of model in a way to determine which subset of models should be applied to a certain input.

This strategy is used because it can accelerate data processing substantially, alternatively individual neural networks can also demonstrate dynamic structure internally by determining which subset of features should be applied over a certain input.

The general idea will be that the final model will be a probabilistic representing the presence of subpopulations within an overall population, without requiring that an observed data set should identify the subpopulation to which an individual observation belongs.

The computation of the softmax function requires three steps: 
- exponentiation of each term
- sum over each row to compute the normalization constant for each example
- division of each row by its normalization constant, ensuring that the result sums to 1

In a similar way we can say that the division of each row by its normalization constant, can be considered in a way similar to the probabilistic model representing the subpopulations.

1. Surrogate models re important for explainable ML. How are they used for that ?

Surrogate models are usually simpler and interpretable models that are used to approximate the behavior of more complex black box models.

They do this by training the surrogate model to mimic the behavior of the complex model over the entire feature space, and given surrogate models are inherently explainable we can then deduce from the interpretation of the surrogate model the interpretation of the black box.

In some situation we aren't required to even use the entire feature space a local approach can be beneficial to explain individual predictions which can have more value than the global state of the prediction space. 

2. Give one example of a ML model that needs a surrogate model for explainability and one that doesn't.

Neural Networks for example require a surrogate model to be explainable given they are the definition of a black box

Decision Trees are inherently explainable and therefore don't require a surrogate model to be explainable, moreover this type of model is usually used as a surrogate model for other ML models.

3. Can data augmentation be used to attack ML models?

Data augmentation is a technique used upon data in which we apply invariant transformations upon existing data, and by which we obtain new data examples. These transformation usually revolve around rotations and transformations.

With this in mind, this approach can be used to prevent attacks upon data models given it defends against poisoning attacks given that in this type of attack, subtly modify or inject malicious data into the training set in order to induce the model into making incorrect predictions.

This approach by making the model more robust to small changes makes this type of attack more difficult to execute.

1. How does regularization work to prevent ML attacks?
 
Regularization is a technique used in machine learning and statistics to prevent overfitting by adding a penalty term to the loss function. Overfitting occurs when a model learns the training data too well, capturing noise in addition to the underlying patterns.

With this in mind, regularization can be used to prevent ML attacks given we are increasing the robustness of our model, this just like data augmentation can defend against multiple types of attacks by making sure the model is more difficultly fooled.

Specifically, poisoning attacks can be easily countered given that overfitting can be seen as a possible attack vector to be exploited in a poisoning attack.