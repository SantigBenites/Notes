# Question 1

## Find the optimal weights w0. Hint: recall that the separation margin between the two classes is ρ = 2/‖w0‖

Lets start by kernelizing the function



# Question 2

## Markov chains can be used in language models. Discuss their limitations in these problems

When using markov chain for language models, we can consider each state a word and each transition the probability of another word appearing.

Take for example, "I ate an apple", in this case "I" and "ate" would be states and the transition would be the probability ate appears after I.

This type fo approach has some limitations:
- The large transition space of spoken language, leads to the chain not being able to present the entire transition table
- The usage of a transition table makes it so the model doesn't understand the language it is reading and only bases his assumptions on probability
- The fact that it only considers the previous state and therefore is unable to get the concept of the phrase
- The entropy rate of spoken language not being enough for the model to be effective


## How would a hidden Markov model modify the previous discussion?

HMM are similar to normal markov chains but some of their states are hidden.
This means they no longer use matrices to map the transitions between states and that transitions are usually based on a model.

With this in mind we can see that when using a HMM for language models, we have some new upsides to consider.

In this case our visible states would still be our words, but instead of depending on a transition matrix to calculate transition values we will use the model to predict the value of our transition.
This means that we solve the 2 first problems with Markov chain.
If no matrix is required for HMM then there is no need to present the entire transition matrix
And the usage of these hidden states allowing the model to understand more complex concepts of language.


## The emission, or observation matrix is related to which kind of Markov model? What does it represent

The emission matrix is used in HMM.

It represents the probability of an observation given a hidden state.

In other words, given an hidden state h(t) in time t, the observation matrix shows the probability of the next hidden state h(t+1).

## Describe one way of obtaining the emission matrix

One way to obtain an observation model is by creating it off a previously known set of data.

Using a set of data which constitutes a transition between states, we can fill the emission value based on the real data we are using to train the model.


# Question 3

## Discuss the influence of the past in recurrent learning machines and in filter machines. Analyze the influence of the order of the memory on this

Normal machine learning models aren't able (usually) to take into consideration time as a factor when making a prediction. This limits them to a certain point to make decisions based on the current data point entry.

When using recurrent learning machines like RNN we can use memory has a method of allowing the model to take into consideration multiple previous entries when making a decision about a datapoint.

To this effect models such as LSTM or GRU are useful not only to allow the NN to obtain the data about previous entries, which it requires to make assertions, but also to scale the value of the data to the appropriate amount, which means to give less importance to datapoints in memory which are further in the past.

## Describe the differences between the positive and negative phases of a Boltzmann machine including their duration and how the latter can be limited

During the training of a boltzmann machine we want to maximize the product of the probabilities that the the Boltzmann machine assigns to the binary vectors in the training set.

This is equivalent to maximizing the sum of the log probabilities that the Boltzmann machine assigns to the training vectors.

This is problematic because in order to know the weight of a certain probability we are going to need to know the weights of previous probabilities.

To do this type of learning we have 2 phases

- The positive phase finds hidden configurations that work well with v and lowers their energies.
- The negative phase finds the joint configurations that are the best competitors and raises their energies.

The first phase is done once for all data vectors, while the seconds is done as many times as needed to get good estimates.

With this in mind, if we decreases the required quality of estimates we can decrease the expected time.