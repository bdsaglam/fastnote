# NLP

## Tokenization
Tokenization is the process of converting a sentence into a sequence of tokens which can be characters, subwords or words depending on the tokenization algorithm. Subword tokenization analyzes the dataset and find common occurrences of subwords to be used as tokens. It is the most effective method and provides the capability of varying the granularity of tokenization by tuning vocab size. Larger vocab results smaller tokens but longer representation for sentences; converging to character tokenization at the limit. Whereas with small vocab size, the tokenizer doesn't split words much, indeed it can even group multiple words into phrases.

fastai uses `spaCy` tokenizer by default.
```py
sp = SubwordTokenizer(vocab_sz=1000)
sp.setup(corpus) # corpus: list of sentences
tokens = sp(['fastai library is great!', 'fastai course is even greater, since it is top-down.'])
```

## Numericalization
It is converting tokens into embeddings; hence, we need to determine the order of tokens.

From fastai course:
> Our special rules tokens appear first, and then every word appears once, in frequency order. The defaults to `Numericalize` are `min_freq=3,max_vocab=60000`. `max_vocab=60000` results in fastai replacing all words other than the most common 60,000 with a special *unknown word* token, `xxunk`. This is useful to avoid having an overly large embedding matrix, since that can slow down training and use up too much memory, and can also mean that there isn't enough data to train useful representations for rare words. However, this last issue is better handled by setting `min_freq`; the default `min_freq=3` means that any word appearing less than three times is replaced with `xxunk`. fastai can also numericalize your dataset using a vocab that you provide, by passing a list of words as the `vocab` parameter.
