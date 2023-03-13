## Recurrent Neural Networks

### Feed Forward Network
- Tradicional model of feed forward networks takes an input and returns an output (without use of memory); (output of neurons in first layer is input of neurons in second layer)

(Connection weight is all that varies during learning process, learning process looks for optimal weight)

### Recurrent Neural Network
- Recurrent neural networks uses feedback loops (outputs are fed back into neurons as inputs, so if they change they create new changes);

Networks with feedback:
-> Local is at the level of the neuron;
-> Global is between parts of the overall network;

We desire stable networks. Networks are trained with Hebb´s rule (explicit training).
(Important aspect of neural networks is to check if network will stabilise at any point)

Associative Learning:
->If two neurons are active at the same time, in the learning process, the weight of their connection grows; (means they are associated)
-> If one neuron is active and the other is inactive at the same time, the weight of their connection diminishes; (means they are not associated)

Dinamical Systems: (didnt go over maths in class)
-> Process is a dinamical system. We want the network to have a basic atraction towards a certain point / direction;
->In recurrent neural networks we want as many basins of attraction as patterns we want it to recognize;

(Two attractions have a splitting line between each other)
(Each attractor has a basin of attraction. Equilibrium is not necessarily static)

Large number of degrees of freedom are the weights of the connections we can manipulate in the network.

-> Associative memory: Store a set of patterns so that when presented with a new pattern, it produces the stored pattern that most closely resembles it;


## Hopfield Networks
- Reccurent networks with a single layer, where all neurons have feedback (each neuron with three inputs and no self input -> means other neurons have feedback to other neurons but not themselves);

Boxes in hopfield network drawing have a simple meaning. Since we are considering discrete networks (time works in steps), the boxes represent the unit time delay (if signal is sent in t then output of box is signal but in time t+1); (difference of one time step)
(Without this (the delays), we would have to compute all convergences in the same time step which in practice, would remove iteration and be very complex)

(We are only studying discrete models of neural networks, although continous models also exist)

The additive model of the neurons looks at the matrix of weights (weights are symmetrics, weight from neuron 1 to neuron 2 is exactly the same as the weight from neuron 2 to neuron 1 -> neurons influence each other in the same way).

(Non linear function is like sigmoide, cant draw here so look it up. The non linear function is invertible and every neuron has a non-linear function)
(Math was mostly skimmed over in class, re-read slides)

-> The fixed point attractors are minima in the energy function and vice-versa;

## Discrete Hopfield Networks
- Use of the additive model, as per the mccullock-pitts networks. Avoids self connections and we set a bias term; (neuron has weights and we also usually have a bias for the neurons, special weight for a constant input of 1 -> allows us to place neuron when it is inactive (working point of the neuron))

States of the neurons can be updated either sinchronously or asynchronously.

(Hebbs rule: neurons that fire together wire together)
(Formula explained: Weight of neuron j to neuron i is based on the weight of both the neurons plus the alpha times the input of neuron j and the input of neuron i)

Sai mi is the ith component of pattern m -> We have patterns to store (m) and we are going to obtain the weight of the neurons by multiplying the sai mi with the sai mj for each pattern. 

To store a pattern, each position of the pattern needs to be associated with 1 neuron; (32x32 pixels image needs to be store in hopfield network with 32x32 neurons) (i component is 1 position of the pattern and the j component is the other position of the patterns)

(Allows us to know the network in one shot if we know the pattern. If we want to store 3 patterns, we just need to go through each pattern and see if the neuron is active and then sum all the patterns) -> (not sure on this part, didnt quite understand)

How many patterns can a network store? Error rate inscreases with more patterns, aproximate capacity is similar to the number of neurons. Symmetry in weights is important for stability. 
Is considered as having noise removal due to the addition of noise to the images being automatically not seen, recovering patterns without noise;

## Self-organising Maps
- Models of competitive learning (unsupervised). Considered competetive as there is only one winner (one neuron that is most active). Process of learning (to stabilise network) uses lateral inhibition (winner pulls down / decreases other neurons so that its considered more of a winner). Neurons are in a grid, usually 2D;

Neurons organise topologically to reflect the statistical characteristics of the training examples (networks are used for clustering purposes, to form clusters of data that are closer to each other than other clusters). Can be seen as non linear generalisation of PCA.

Desirable property (of maps):
-> Preservation of topology. Neighbouring patterns map to neighboring neurons; (Which is why its good at representing brain stuff)

Uses:
-> Clustering;
-> Detecting novelties in an input space;
-> Easy to observe visually;

### Models
- Only see the kohonen maps as they are simpler to analise and much more used than other models;

#### Kohonen Maps
- Input layer (input neurons) and the network layer (computational layer / output layer) where all the inputs are connected to the all neurons in the output layer; (feed forward network, model is more general than wilshaw model)

(Learning is done by changing the weights of the connections)

Training process:
-> Initialisation; Assign small random values to the weights;
-> Competition: For every input pattern calculate the value of the discriminant for each neuron, and highest value is the winner (neuron that is topologically closest to the pattern);
-> Cooperation: Winning neuron defines a spatial neighborhood for other neurons that can adapt (winning neuron chooses adaptation neighborhood with is where neuron weights will adapt, closest ones will move closer to input, further away they are the less they move);
-> Synaptic Adaptation: More excited neurons increase their discriminant values, relative to the input pattern;

Each neuron is a vector in the input space and their geonmetic position is the ouput. During training, neurons are pulled towards the position of their closest input patterns.

(Present one point, see what neuron has the highest activation value then pull that neuron towards that point. This starts, as seen in the first image, unfold into a line from the cluster it previously was -> learning process starts to unfold the network so that it corresponds to all the points in the triangle)

How to know if map is well trained: (neurons can get twisted, points that should be further apart are closer)
-> Can be prevented by running the process more than once or by adding random small values;


## The 3 component mechanisms
- Neurobio analogy (neural activity tends to excite neighbors more than distant neurons). Learning process needs to know each neuron and their neighbors;

(Neighborhood is a unimodal function, meaning it only has one maximum / minimum)

Neighborhood of hj,i decreases with time, meaning neighborhood function is going to squeeze for a long time until it basically only affects the winning point.

(Use of a modified Hebb rule to prevent saturation - use of an ether (weird symbol) to add learning process -> cant be too high or too low)

Result:
-> Topological ordering of the features of the input space means adjacent neurons in the grid tend to have similar weight; (winner affects more neighbors in the grid than distant neurons;

Summary:
(Went too fast, couldnt get it, just use slides)

## Properties
- Instead of five inputs we have two inputs (points in space). We are mapping these points in the space to the network. We compute the product by the weight of the neuron, if weights are of similar dimension (nearly identical) then weight is representation of input space. Winning neuron doesnt need to be identical to weight; (grid regions in input space)

## Example
- Seen applications and work of teachers student;

### Students Work
- Suppose we have a cube, with coordinates starting at 0,0,0 and ending at 100,100,100. What the student did was to create random points around the vertixes of the cube (for each vertix, create 100 random points with a gaussian distribution around the 3 axis). This generates a cloud of points around the vertixe, giving the training set 8 clouds of points; (training set)

We would expect that the kohonen map reflects the 8 clusters and he made a video reflecting the visualization of this in a 3D environment with a 2D network. So he had to use the points in a 2D network to a 3D space using their weights while maintaining their connections.  (see video if in slides, not sure)

In these cases, there is no labeling. We only provide the example and the networks does what it can with that example. Network isnt given any other information other than example.

## Back Propagation (MLP -> Multilayer Preceptron)
- Feed forward network with several layers. Hidden layers inbetween (between input and ouput) as observer has no access / visualization of whats happening in between; (Not really sure what this whole topic has to do with class, teacher using other slides (from advanced machine learning) so if he makes those available il have to check it out again)

(Single layer preceptron can not solve non linearly seperable problems -> XOR logical function)

Most common learning model is the error backpropagation model.
Two steps:
-> Forward step: Provide an input to the network and output is computed; (by forward propagation with constant weights)
-> Backwards step: Weights are adjusted from an error signal; (error is the difference between the real ouput and the desired output)

Backprop is a computationally efficient learning algorithm.

