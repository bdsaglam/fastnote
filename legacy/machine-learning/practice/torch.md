
## Reset GPU memory
```py
torch.cuda.reset_max_memory_cached()
torch.cuda.reset_max_memory_allocated()
torch.cuda.reset_accumulated_memory_stats(
```

## Get torch device
```py
device = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")
```