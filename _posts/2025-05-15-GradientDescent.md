# Understanding Neural Networks

I was going over this ![this notebook](https://github.com/lovellbrian/course22/blob/master/04-how-does-a-neural-net-really-work.ipynb) trying to get an understanding of gradient descent and neural networks.

From what I understand know, neural networks are composed of layers which:
1. Accept and process inputs by multiplying them by weights and biases
2. Add the inputs together
3. Set any negative results to zero

This general process is repeated for each layer, with the inputs of previous layers acting as inputs to new ones.
However, to do useful work, we need some way to change the values of the weights and bias parameters.
This is what gradient descent allows us to do. By expressing the mean absolute error between our current and desired value in terms of our parameters, we can take the derivative of our absolute error and adjust the parameters so that we travel in the direction of decreasing derivative. Eventually, we'll reach a minimum value at which the derivative is zero and **the absolute error is minimised**. This is gradient descent: we're descending the gradient.

---

To produce a neural network, we want to find a way to *automate* this process. We can do this by calculating the partial derivatives of our loss function with respect to each weight and adjusting the weights in the direction opposite the sign of the gradient.
The trick to doing this is to **backpropagate** the gradient, multiply it by a small value, and subtract it from the weights. Since the gradient is negative, the subtraction will icncrease the value of the weights and decrease the gradient further. We can continue doing this until we reach the minimum loss.

The small number that was multiplied with the gradient is the **learning** rate of the system. The learning rate is a crucial variable, as it controls the speed at which we approach the minimum loss. Making the learning rate too high can increase the weights too much, causing the gradient to leave its local minima. Leaving the learning rate too low will signficiantly slow the speed at which we can reach the minimum loss.

---

Gradient descent forms the basis for deep learning since it allows us to mitigate the loss for any mathematical system with single input, and with sufficient layers, *most* things can.
