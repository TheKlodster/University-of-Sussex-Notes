*Lectures 7 & 8, 18th & 19th February*
# Neural Networks

### Single Perceptron
--------------------------------------------------
Components of a General Artifical Neuron:
1. A set of inputs.
1. A set of weights.
1. A bias.
1. An activation function.
1. Neuron output.

The output is the classification: binary (0 or 1), or (-1 or 1). <br>
Parameters: the threshold *f* is a parameter, and all the weights *w*.

The **discriminant is always linear for single neuron perceptrons!** i.e. output *y* depends only on a linear function of the inputs.

The perceptron sums all the inputs, weighting each one according to the weige paramters, and then classifies according to whether or not the sum exceeds the threshold of the activation function.

Perceptron can do supervised learning, by updating the weights using gradient descent.

#### Learning Training
Standard procedure for training the weights is by **gradient descent**. <br>
Take a set of training data from known classes, and use an error function E(w) to specify an error for each sample.

#### Error for Perceptron
E(w) = 0 when the classification is correct. <br>
When wrong, the error is how far the perceptron was from getting it right.
<center>

E(w) = w * x  : if output is +1 and output should have been -1. <br>
E(w) = - w * x  : if output is -1 and output should have been +1.

</center>

### Multi-Layered Perceptron

<center>

<img src="https://images.deepai.org/glossary-terms/49157de013394ab7a36022759a55b6aa/multipercep.jpg">

</center>

Single layer generates a linear decision boundary. But what if that doesn't make sense for your data?

*Minsky* and *Papert* (1969) offered a solution to the XOR problem by combining perception unit responses using a second layer of units.

**XNOR Gate**

#### Properties of Architecture
- No connections within a layer.
- No direct connections between input and output layers.
- Fully connected between layers.
- Often more than 3 layers.
- Number of output units need not equal number of input units.
- Number of hidden units per layer can be more or less than input or output units.

#### What do each of the layers do?
1. 1st Layer draws linear boundaries.
1. 2nd layer combines the boundaries.
1. 3rd layer layer generates complex boundaries (large 2nd layer can technically do anything, but in many cases more efficient to have more than 1 hidden layer).
