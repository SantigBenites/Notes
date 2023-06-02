# Question 1

## Find the optimal weights w0. Hint: recall that the separation margin between the two classes is ρ = 2/‖w0‖

Lets start by kernelizing the function



# Question 2

## Markov chains can be used in language models. Discuss their limitations in these problems

When using markov chain for language models, we can consider each state a word and each transition the probability of another word appearing.

Take for example, "I ate an apple", in this case "I" and "ate" would be states and the transition would be the probability ate appears after I.

This type of approach is normally used initially when trying to do language models, but it is usaully dropped beacuse of some limitations:
- The large transition space of spoken language, leads to the chain not being able to present the entire transition table
- The entropy rate of spoken language not being enough for the model to be effective


## How would a hidden Markov model modify the previous discussion?

HMM are similar to normal markov chains but some of their states are hiddenm