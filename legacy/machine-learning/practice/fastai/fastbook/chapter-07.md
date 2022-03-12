# Sizing and TTA (tips for higher performance)

## Normalize
When using pretrained models, do not forget applying the same preprocessing (e.g. normalization) the data with stats of the original dataset.

```py
db = DataBlock(
    blocks=(ImageBlock, CategoryBlock),
    get_items=get_image_files, 
    get_y=using_attr(RegexLabeller(r'(.+)_\d+.jpg$'), 'name'),
    splitter=FuncSplitter(lambda o: o.parent.name=='validation'),
    item_tfms=Resize(460),
    batch_tfms=[*aug_transforms(size=224, min_scale=0.75)),
                Normalize.from_stats(*imagenet_stats)]
)
```


## Progressive resizing

Gradually using larger and larger images as you train.


```py
dls = get_dls(bs=128, image_size=128) # implement this utility function
learn = Learner(dls, xresnet50(n_out=dls.c), loss_func=CrossEntropyLossFlat())

# start training with small images
learn.fit_one_cycle(4, 3e-3)

# replace learner's dls with larger images and resume training with fine-tune
learn.dls = get_dls(bs=64, image_size=224)
learn.fine_tune(5, 1e-3)
```

## TTA
Test Time Augmentation (TTA): During inference or validation, creating multiple versions of each image, using data augmentation, and then taking the average or maximum of the predictions for each augmented version of the image.

## Label smoothing

Smooth labels by making likelihood `eps/C` for false labels' and `1 - eps*(C-1)/C` for true label, where `C` is number of classes.
