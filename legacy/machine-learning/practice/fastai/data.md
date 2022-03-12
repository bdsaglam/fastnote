
It's quite easy to use torch datasets and dataloaders.
https://muellerzr.github.io/fastblog/2021/02/14/Pytorchtofastai.html

```py
from fastai.optimizer import OptimWrapper
from torch import optim
from fastai.data.core import DataLoaders
from fastai.learner import Learner
from fastai.callback.data import CudaCallback


def opt_func(params, **kwargs): 
    return OptimWrapper(optim.SGD(params, lr=0.001))

# load torch dataset as usual
dset_train = torchvision.datasets.CIFAR10(root='./data', train=True,
                                        download=True, transform=transform)
dset_test = torchvision.datasets.CIFAR10(root='./data', train=False,
                                       download=True, transform=transform)
# create torch dataloaders
trainloader = torch.utils.data.DataLoader(dset_train, batch_size=4,
    shuffle=True, num_workers=2)
testloader = torch.utils.data.DataLoader(dset_test, batch_size=4,
                                         shuffle=False, num_workers=2)

# create a fastai `DataLoaders` object from torch dataloaders
dls = DataLoaders(trainloader, testloader)

# train the model
criterion = nn.CrossEntropyLoss()
learn = Learner(dls, net, loss_func=criterion, opt_func=opt_func, cbs=[CudaCallback])
learn.fit(2)

```

## image augmentation
```py
aug_transforms(
    mult=1.0, 
    do_flip=True, 
    flip_vert=False, 
    max_rotate=10.0, 
    min_zoom=1.0, 
    max_zoom=1.1, 
    max_lighting=0.2, 
    max_warp=0.2, 
    p_affine=0.75, 
    p_lighting=0.75, 
    xtra_tfms=None, 
    size=None, 
    mode='bilinear', 
    pad_mode='reflection', 
    align_corners=True, 
    batch=False, 
    min_scale=1.0
)
```