# Collaborative Filtering

## Model
A simple neural network which concatenates embeddings

```py
class CollabNN(Module):
    def __init__(self, user_sz, item_sz, y_range=(0,5.5), n_act=100):
        self.user_factors = Embedding(*user_sz)
        self.item_factors = Embedding(*item_sz)
        self.layers = nn.Sequential(
            nn.Linear(user_sz[1]+item_sz[1], n_act),
            nn.ReLU(),
            nn.Linear(n_act, 1))
        self.y_range = y_range
        
    def forward(self, x):
        embs = self.user_factors(x[:,0]),self.item_factors(x[:,1])
        x = self.layers(torch.cat(embs, dim=1))
        return sigmoid_range(x, *self.y_range)
```


Fastai provides a utility function to get good embedding sizes.
```py
embs = get_emb_sz(dls)
```

Fastai also provides a specific learner for collaborative filtering tasks, which can create a neural network automatically.
```py
learn = collab_learner(dls, use_nn=True, y_range=(0, 5.5), layers=[100,50])
```


## delegates
Use `@delegates` decorator to keep function signature when subclassing or decorating other functions.

```
# doc(delegates)
delegates(to=None, keep=False, but=None)
:replace **kwargs in signature with params from to
```

```py
@delegates(TabularModel)
class EmbeddingNN(TabularModel):
    def __init__(self, emb_szs, layers, **kwargs):
        super().__init__(emb_szs, layers=layers, n_cont=0, out_sz=1, **kwargs)
```