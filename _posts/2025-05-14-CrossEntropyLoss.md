# Understanding Cross Entropy Loss

For the multiclassification problem on identifying pet breeds, cross entropy loss was used as the loss function. Since I'm trying to make a multiclass model myself that uses cross entropy, I wanted to gain a better understanding around what it is and how it works.

By reading the ![Fastai course](https://github.com/lovellbrian/fastbook/blob/master/05_pet_breeds.ipynb), I've learned that cross entropy loss is composed of two components:
- A softmax activation function;
- and computing the negative log liklihood.

## Softmax
Softmax is available as a python function:
```python
def softmax(x): return exp(x) / exp(x).sum(dim=1, keepdim=True)
```
Softmax is similar to sigmoid in that it can bound the activation for a class between 0 and 1; however, softmax has the advantage of working with multiple classes. The key feature of softmax is that it is able to bound the acitvations of multiple categories between 0 and 1 such that the activation value of each class adds to one. Since the softmax function takes the exponentital of the activation values, minor differences in activation value are magnified, making it more clear which class has the highest probabiltiy of occuring out of multiple.

## Log Liklihood
Log liklihood is also available as a python function:
```python
nll_loss
```
However, this function does not acutally compute the log: instead, you need to take the ```log``` of the input prior to parsing it into the function or use ```log_softmax```. The effect of taking the negative log liklihood of the softmax activation value is that the resulting loss of the true class is very large if it is close to zero and low if it is close to one. This penalizes the model heavily for making strong incorrect predictions.


By taking the mean of the negative log likelihood, the cross entropy loss is calculated. Cross entropy loss is also available as the python function ```nn.CrossEntropyLoss```. Another useful property of cross entropy loss is that its gradient is linear, resulting in a smoother gradient descent and training loop.
