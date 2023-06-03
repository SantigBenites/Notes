# Question 1

## Identify the main pros and cons of Q-learning as a dynamic programming method.

We consider dynamic programming in this context as a mathematical formulation of planning a multistage sequence of actions for an agent in a stochastic environment.

If we consider this definition, this concept doesn't deviate much from normal reinforcement learning, considering in reinforcement learning we are try8ing to get a agent to learn to navigate an environment.

Considering Q-learning is an implementation of a reinforcement learning algorithm we can see how this approach would be intrinsically related with dynamic programming.

The main pros of Q-learning are:
- The ability to use a non-stationary policy
- Is able to find an optimal policy
- Is able to use exploration/exploitation

The main cons of Q-learning are:
- Requires exploration of the entire input space
- If using table, is limited by table space, and cant be used in big input spaces
- Has a e-greedy policy
- Needs to explore state-action a significant amount of times


## Dynamic programming requires a greedy policy with respect to the optimal cost-to-go function. Why does not Q-learning strictly apply this policy, and instead uses an asymptotic approach to it?

Q-learning doesn't strictly apply a greedy policy, it uses a epsilon-greedy policy.

This type of policy is used in order to make the system more effectively apply the concept of exploration-exploitation.

This is made because in Q-learning, so that the algorithm has a better balance between trying to optimize the best solution to the problem(exploitation), and make efforts to find alternative solutions which might be better than the current best (exploration).

## Analyze the the influence of the temperature parameter in a Boltzmann (soft-max) action choice in Q-learning


The temperature parameter in a Boltzmann action choice is used as an input for the function

$$ p(a|s) = \frac{e^{( - \frac{Q(s,a)} {t} )}} {\sum_{a'} e^{(\frac{Q(s,a)} {t}) '}}$$

It substitutes part of the energy function of a normal boltzmann.

It servers as a measure of the amount of exploration the algorithm should do.

If T is high then it will do a lot of exploration, if T is low then it will choose the action with best Q value.

## Why is reinforcement learning considered an unsupervised form of learning although some cost information is provided?

Unsupervised learning is a type of machine learning where the machine is given a set of training data which is unlabeled.

Reinforcement learning is considered a type of unsupervised learning, even though it has a cost function, given it doesn't label the data priori, the values of the cost function only allow the agent to make assertions regarding its current state.

This means that depending on the algorithm different optimal solutions may be found, given the algorithm conducted itself in different ways.

This being said considering RL a form of unsupervised learning is no longer the norm considering the substantial amount of differences between these 2 paradigms.

# Question 2

## Suppose you are consulted about using a boosting approach in a specific problem. What kind of problem would prompt you to recommend that approach? How would you decide between recommending filtering or re-sampling forms?

Considering boosting is a algorithm that trains experts sequentially using different data on each one and that requires experts to be weak learning algorithms.

I would say, that our problem should be simple enough that weak learning models could solve it and so that sequentially learning models wouldn't take too long.

Re-sampling and filtering are 2 approaches to implementing boosting.

Filtering we need to have an unlimited dataset, but we have low memory usage

Re-sampling we doesn't need a infinite dataset considering we can reuse the training set, but this influences the model so its performance is bounded.

Therefore depending on the size of our dataset and the performance of our model both in terms of accuracy and in terms of memory management the appropriate approach should be chosen.


## Adaboost needs week learning algorithm. Explain what is such an algorithm

Weak learning algorithms are defined as algorithms which only need to work slightly better than random choice.

These types of algorithms are favorable to Adaboost considering that while this type of approach has a large error on his own, when used inside a ensemble model they become more robust and more effective.

## What is the weight Adaboost considers for a learner that has an error e = 0.5?

Considering the weight of a model is based on calculating the value with the least amount of error, and assuming all models worst possible case is that they are only 50% accurate.

We can conclude that the weight of this learner would be 0.

We can confirm using the equation for the weight

$$ B_n = \frac{1}{2} * ln(\frac{1-e_n}{e_n}) = \frac{1}{2} * ln(\frac{1/2}{1/2}) = \frac{1}{2} * ln(1) = \frac{1}{2} * 0 = 0$$


## The K-means can be implemented with Expectation-Maximisation. What is the stopping condition of this learning algorithm?

K-means and EM are 2 methods to assign points to specific clusters.

Therefore while they can be used in conjunction one cannot be implemented using the other.

To this effect the stopping condition of k-means will be when the silluete of the data provides a good measure of cluster quality