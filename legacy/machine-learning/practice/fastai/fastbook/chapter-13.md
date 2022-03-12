# CNN

- Activation size formula
```py
activation_size = (image_size - kernel_size + 2*padding) // stride + 1
```

We want to have more output features from convolution layers and the way to do 
that is to increase the number of filters. 
Since the number of output channels directly proportional to the number of input channels, 
we need to increase number of filters in the first conv layer. 
However, if we increase it too much, then conv layer may not learn anything useful. 
For example, in a grayscale image, a kernel with size of 3 will take 9 pixels as input, and 
if we have 9 filters then it doesn't have to learn anything from input.
It can just copy input to output. Hence, we use larger kernels at the beginning of CNNs.


- Monitor activation stats during training

```py
learn = Learner(dls, cnn(), loss_func=F.cross_entropy,
                    metrics=accuracy, cbs=ActivationStats(with_hist=True))
learn.fit_one_cycle(epochs, lr)
learn.activation_stats.plot_layer_stats(-2)
learn.activation_stats.color_dim(-2)
```