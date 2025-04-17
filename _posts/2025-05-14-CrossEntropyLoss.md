# Understanding Cross Entropy Loss

For the multiclassification problem on identifying pet breeds, cross entropy loss was used as the loss function. Since I'm trying to make a multiclass model myself that uses cross entropy, I wanted to gain a better understanding around what it is and how it works.

By reading the ![Fastai course](https://github.com/lovellbrian/fastbook/blob/master/05_pet_breeds.ipynb), I've learned that cross entropy loss is composed of two components:
- A softmax activation function;
- and computing the log liklihood.

## Softmax
Softmax is available as a python function:
```python
def softmax(x): return exp(x) / exp(x).sum(dim=1, keepdim=True)
```
Softmax is similar to sigmoid in that it can bound the activation for a class between 0 and 1; however, softmax has the advantage of working with multiple classes. The key feature of softmax is that it is able to bound the acitvations of multiple categories between 0 and 1 such that the activation value of each class adds to one. Since the softmax function takes the exponentital of the activation values, minor differences in activation value are magnified, making it more clear which class has the highest probabiltiy of occuring out of multiple.

## Log Liklihood
Log liklihood is also available as a python function:

