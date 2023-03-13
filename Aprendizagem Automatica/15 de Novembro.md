# Linear Separable Data

Labeled data is categorized as linearly separable if there exists a linear decision boundry which can separate the data into classes
This linear decision boundry can be 100% accurate, but it isnt required nor is it the norm
This labeled data can accept a multitude of linear sepraration boudnrys, but some will be obviosly better than others

# Support Vector Machines

TO enable us to more easily predict valid linear decision bounrdys we can create support vectors for the problem.
Suport vectors are training examples neartest the decision boundry, and are used to create an area where the decision boundry can exist and have a valid accuracy

*See slides for good image*

## Maximizing the Margin

It is therefore our objective to not only have a valid margin, but also to have the biggest margin possbile, therefore we must try to maximize the margin of w.
To do this, it is obvious that in order to maximize the margin we must minimize ||w||,  provided that none of the trail points falls under the margin.
This problem can now be solved using a quadratic constraint problem.
"consider that ||w|| is the norm of w, and therefore it is perpedicular to w"
Considering we are searching for the best possbiel amrgin until we find the suport vector(the first example for the class), we can say that more than searching for the best possible margin, we are also searching for the best support vector.

# Kernels

Kernel methods are usually used in support vector machines.
A kernel method is a fucntion that is applied as a dot product to the optimiztion problem, the best thing is that these kernel methods are just reltionships between isntances and dont alter the actual problem.

In essence we use kernel mthods to transform non linear spaces into linear ones, so that we can use linear separation problem.
