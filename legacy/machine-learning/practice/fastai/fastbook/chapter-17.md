# Foundations


Backpropagation of linear layer
```
# y.shape = hout
# x.shape = hin
# w.shape = (hout, hin)
# b.shape = hout

y = x @ w.t + b
dy/dx = w.t
dy/db = ones_like(b)

dy/dw = x.tile(hout, 1) # (hout, hin)

dloss/dx = dloss/dy @ (dy/dx).T # (hout,) @ (hout, hin) = (hin, )
```

Further reference
http://cs231n.stanford.edu/handouts/linear-backprop.pdf