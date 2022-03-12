
# tips, tricks, quirks

- pipeline components are not fitted though pipeline is fitted
https://stackoverflow.com/questions/58704347/sklearn-components-in-pipeline-is-not-fitted-even-if-the-whole-pipeline-is

Make sure to use `transformers_` or `named_transformers_` when getting fitted transformers of a `ColumnTransformer`.