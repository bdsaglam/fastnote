# Mid-level API

These two code block does the same job; the first with by the mid-level API and 
the second with high level (DataBlock) API.

Mid-level
```py
path = untar_data(URLs.IMDB)
xtfms = [Tokenizer.from_folder(path), Numericalize]
ytfms = [parent_label, Categorize]
tfms = [xtfms, ytfms]
files = get_text_files(path, folders = ['train', 'test'])
splits = GrandparentSplitter(valid_name='test')(files)
dsets = Datasets(files, tfms, splits=splits)
dls = dsets.dataloaders(dl_type=SortedDL, before_batch=pad_input)
```

High-level
```py
path = untar_data(URLs.IMDB)
dls = DataBlock(
    blocks=(TextBlock.from_folder(path),CategoryBlock),
    get_y = parent_label,
    get_items=partial(get_text_files, folders=['train', 'test']),
    splitter=GrandparentSplitter(valid_name='test')
).dataloaders(path)
```