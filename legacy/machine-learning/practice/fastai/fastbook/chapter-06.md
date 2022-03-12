# Multi-label classification

# Binary cross entropy loss
We can't use PyTorch's `CrossEntropyLoss` since it applies softmax and pushes down all probabilities to zero except one true class; whereas in multi-label classification, we may have multiple 1's in target. Hence, we should use `BCEWithLogitsLoss`, which applies `sigmoid` to logits and then applies binary cross entropy loss.

```py
def binary_cross_entropy(inputs, targets):
    inputs = inputs.sigmoid()
    return -torch.where(targets==1, 1-inputs, inputs).log().mean()
```