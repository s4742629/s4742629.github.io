# Useful Plots for Improving Model Performance

![The jupiter notebook for classifying pet breeds](https://github.com/lovellbrian/fastbook/blob/master/05_pet_breeds.ipynb) has provided me with many useful plots I can use to better understand and optimize the performance of my model.

## Confusion Matrices
```python
interp = ClassificationInterpretation.from_learner(learn)
interp.plot_confusion_matrix(figsize=(12,12), dpi=60)
```
The confusion matrix is a useful tool for visualising the performance of a model. Using a confusion matrix, it is easy to tell the number of succesful identifications against the number of misidentifications.

## Loss Over Time
```python
learn.recorder.plot_loss()
````

![](/Capture6.JPG)

By plotting training and validation loss of the model over time, we can determine whether the number of epochs that the model is trained for is sufficient or not. Ideally, the number of epochs the model is trained for should be great enough so that the training loss fully declines before slowing and planteauing. At this point, the decrease in training loss has diminished as the model begins to over fit. Additionally, during this time, the validation loss will fluctuate, sometimes rising. Despite this, the accuracy of model should continue to improve so long as the model doesn't become too over fit and begins incorrectly memorizing training data. Generally, training the model for more epochs will result in better accuracy but the main cost associated will be time.

## Loss Over Learning Rate
```python
learn = vision_learner(dls, resnet34, metrics=error_rate)
learn.fine_tune(1, base_lr=0.1)
```

![](/Capture6.JPG)

To optimise the learning rate, we can construct a learning rate finder. Beginning at a very low learning rate, we can progressively increase the learning rate and observe the change in loss, watching loss decrease before the learning rate becoomes too high and loss spikes. From the resulting graph we can select a learning rate for our model between the centre of the slope and the minima, decreasing the loss as much as possible without letting the learning rate become too high.

### Freezing and Fine Tuning
The notebook also discusses the concept of freezing network layers wherein a pretrained model has its final classifcation layer removed and replaced with randomly weighted/biased layers and has the rest of its weights and biases frozen. Since the rest of the model has been frozen and specifically trained for high performance, all changes to reduce loss are placed on the weights and biases of the final layers. Cosnequently, instead of uising random weights and biases for the final layer, the intial weights and biases can be selectively chosen to improve the performance, fine tuning it. This is usually done by training  the mdoel with the majority of it  frozen before unfreezing it and training as usual for several epochs.

### Discriminative Learning Rates

![](/Capture6.JPG)

Employing discriminative learning rates is another method by which performance can be improved wherein the learning rate is varied across the layers of the network. Since earlier layers in a network focus on training basic shapes while later layers focus on more complex structures, varying the learning rate can prove advantageous as it allows more basic layers to train faster while providin enough finess for more complex layers.

## Deeper Architecture
A simple way of improving model preformance is to switch to a neural network architecture with more parralel layers, such as switching from a resnet18 to resnet34. The increased number of layers in the new neural network has the advantage reducing overall loss but increases GPU load and suceptibility to over fitting.
