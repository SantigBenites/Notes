
Exercise 1

Lets start by calculating the values of each neuron
For Neuron 1 we have
$$ Neuron1 = x_1 * w_{11} + x_2 * w_{12} + b_1 \iff Neuron1 = x_1 * 1 + x_2 * 1 - 1.5 \iff Neuron1 = x_1 + x_2 -1.5$$
and for Neuron 2 we have
$$ Neuron2 = x_1 * w_{21} + x_2 * w_{22} - 0.5+  Neuron1 * w_{23} \iff Neuron2 = x_1 + x_2 - 0.5 + Neuron1 * -2 $$
Lets also consider that the neurons in question are using a step function so that
$$
\begin{cases}
  x > 0 = 1\\    
  x \le 0 = 0    
\end{cases}
$$
With all of this considered lets start analysing the NN

a)
A McCulloch-Pitts neuron will work in such a form, considering both neurons will work like this we must take into account for the margin of Neuron2 the step function in Neuron1
![[McCulloch-Pitts.png]]

To calculate the separation boundary of our NN we must take into account the step function operating on each neuron individually.
For this lets calculate the values in which the value of Neuron1 passes from positive to negative.

This means that solving the equation $0 = x_1 + x_2 -1.5$ gives us a separation boundary
Solving this equation gives us the first decision boundary $x_1 + x_2 = 1.5$

Now lets consider the separation boundary of the second neuron.

This means also solving a similar equation but in this case it will be $Neuron2 = x_1 + x_2 - 0.5 + Neuron1 * -2$, and we must take into account the value of Neuron1 in the calculation.

For this we must calculate the boundary when the value of Neuron1 is equal to 1 or 0.
This can be done by solving the following equations

$$
\begin{align}
x_1 + x_2 - 0.5 + Neuron1(0) * -2 = 0 \leftrightarrow x_1 + x_2 - 0.5 + 0 * -2 = 0 \leftrightarrow x_1 + x_2 - 0.5 = 0 \leftrightarrow x_1 + x_2 = 0.5 \\
x_1 + x_2 - 0.5 + Neuron1(1) * -2 = 0 \leftrightarrow x_1 + x_2 - 0.5 + 1 * -2 = 0 \leftrightarrow x_1 + x_2 - 0.5 + -2 = 0 \leftrightarrow x_1 + x_2 = 2.5
\end{align}
$$
Considering the values of $x_1$ and $x_2$ can only be $\in\{0,1\}$ we can see that $x_1 + x_2 = 2.5$ is impossible
Therefore we can just reduce our decision boundary to the following equations
$$
\begin{align}
  x_1 + x_2 = 0.5\\    
  x_1 + x_2 = 1.5
\end{align}
$$

b)

To try to calculate the truth table for this NN we must only make a table for all possible values of input that the NN can have therefore considering that $x_1$ & $x_2$ can only have the inputs of 0 and 1, the truth table will be as follows

| $x_1$ | $x_2$ | N1                            | N2  | NN value |
| ----- | ----- | ----------------------------------------| --- | -------- |
| 0     | 0     | $\psi\{0 + 0 - 1.5\} = \psi\{-1.5\} = 0$ | $\psi\{0 + 0 - 0.5 + 0 * -2\} = \psi\{-0.5\} = 0$  | 0         | 
| 1     | 0     | $\psi\{1 + 0 - 1.5\} = \psi\{-0.5\} = 0$ | $\psi\{1 + 0 - 0.5 + 0 * -2\} = \psi\{0.5\} = 1$   | 1        |
| 0     | 1     | $\psi\{0 + 1 - 1.5\} = \psi\{-0.5\} = 0$ | $\psi\{0 + 1 - 0.5 + 0 * -2\} = \psi\{0.5\} = 1$   | 1        |
| 1     | 1     | $\psi\{1 + 1 -1.5\} = \psi\{0.5\} = 1$ | $\psi\{1 + 1 - 0.5 + 1 * -2\} = \psi\{-0.5\} = 0$   | 0        |
