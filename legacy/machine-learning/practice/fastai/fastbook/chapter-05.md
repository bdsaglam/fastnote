# Pets

## Datablock
It's very easy to create PyTorch datasets and dataloaders with Fastai's DataBlock API.

```py
pets = DataBlock(
    blocks = (ImageBlock, CategoryBlock),
    get_items=get_image_files, 
    splitter=RandomSplitter(seed=42),
    get_y=using_attr(RegexLabeller(r'(.+)_\d+.jpg$'), 'name'),
    item_tfms=Resize(460),
    batch_tfms=aug_transforms(size=224, min_scale=0.75)
)
dls = pets.dataloaders(path/"images") # dls.train, dls.valid
dls.train.show_batch(nrows=1, ncols=3)
```

## Learners
Fastai provides several specialized learner implementations for different modalities, such as `cnn_learner` for vision problems; hence, we don't have to implement it ourselves from `Learner` class.

```py
learn = cnn_learner(dls, resnet34, metrics=error_rate)
```

## Learning rate finder
Find good learning rate.
```py
lr_res = learn.lr_find()
```

## Fine-tuning
When we create a model from a pretrained network fastai automatically freezes all of the pretrained layers for us. When we call the `fine_tune` method fastai does two things:

- Trains the randomly added layers for one epoch, with all other layers frozen
- Unfreezes all of the layers, and trains them all for the number of epochs requested

We can specify number of epochs for frozen phase.
```py
learn.fine_tune(6, freeze_epochs=3)
```

## Fit one cycle
If we need more control on learning rates and unfreezing with, we can use `fit_one_cycle` method.

```py
learn = cnn_learner(dls, resnet34, metrics=error_rate)
learn.fit_one_cycle(3, 3e-3)
learn.unfreeze()
# discriminative learning rates among layers with lr_max
# earlier layers have smaller learning rates.
learn.fit_one_cycle(12, lr_max=slice(1e-6,1e-4)) 
```
## Training recorder
```py
learn.recorder.plot_loss()
```

## Interpretation of errors
Calculate and plot confusion matrix.
```py
#width 600
interp = ClassificationInterpretation.from_learner(learn)
interp.most_confused(min_val=5)
interp.plot_confusion_matrix(figsize=(12,12), dpi=60)
```