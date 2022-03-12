# Chapter 2 - Production

## Drive Train Approach

Drive train approach for data products focus on infering actions and enabling simulation instead of predictions and forecasting. 
https://www.oreilly.com/radar/drivetrain-approach-data-products/

## Jupyter notebooks

**Jupyter** notebooks are great for experimenting and immediately seeing the results of each function, but there is also a lot of functionality to help you figure out how to use different functions, or even directly look at their source code. 

```
??verify_images
```
a window will pop up with:
```
Signature: verify_images(fns)
Source:   
def verify_images(fns):
    "Find images in `fns` that can't be opened"
    return L(fns[i] for i,o in
             enumerate(parallel(verify_image, fns)) if not o)
File:      ~/git/fastai/fastai/vision/utils.py
Type:      function
```


`fastai` library is written in notebooks, so it's easier to look at notebooks and understand implementations.

## Baseline

Always, create a baseline first when solving a machine learning problem. It can be as simple as infering based on mean of classes. The purpose of this is that we can compare more complex machine learning models to the baseline and assess its success. For example, on MNIST dataset, a baseline may infer the digit by calculating pixel distance between an instance to the mean of all instances in each class. This is one of the simplest model we can have for MNIST problem and more complex models we may create such as a CNN, must perform better than the baseline. So, a baseline provides a lower bound for the task and we can disregard any more complex solution that cannot pass it.