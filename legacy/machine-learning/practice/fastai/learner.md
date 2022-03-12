# Learner

A `Learner` object contains four main things: the model, a `DataLoaders` object, an `Optimizer`, and the loss function to use. 

learn = Learner(dls, model, loss_func=MSELossFlat())

## Learning rate scheduler 
fastai learner uses 1-cycle policy proposed by Leslie for learning rate scheduling.

From fastai paper:
> In all those applications, the Learner obtained gets the same functionality for the model training. The recommended way of training models using a variant of the 1cycle policy [12] which uses a
warm-up and annealing for the learning rate while doing the opposite with the momentum parameter.