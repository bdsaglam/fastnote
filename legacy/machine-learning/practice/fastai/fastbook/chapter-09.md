# Tabular data
https://colab.research.google.com/github/fastai/fastbook/blob/master/09_tabular.ipynb

## TabularPandas
```py
cond = (df.saleYear<2011) | (df.saleMonth<10)
train_idx = np.where( cond)[0]
valid_idx = np.where(~cond)[0]
splits = (list(train_idx),list(valid_idx))
cont,cat = cont_cat_split(df, 1, dep_var='target')
to = TabularPandas(df, procs, cat, cont, y_names=dep_var, splits=splits)
```

## Exploratory data analysis
Traditionally, exploratory data analysis is done before training a model on tabular datasets. This is both time consuming and difficult for feature rich datasets. Fastai suggests training a simple model after a short exploration and cleaning up of data to understand which features are important and what they stand for semantically. It can also help us to identify data leakage.

## Data leakage
Data leakage happens when in training set, input features contain some direct information about target (dependent variable). In such case, the model exploits this and doesn't learn much else. The problem is that data leakage only happens in training set and not present in test set. Therefore, the model performs badly in production. An example is having missing values for a specific category because it's not filled during data preparation. Or fillling some part of the data after the target is realized, e.g. filling some attributes for successful applicants after the application is evaluated. These kind of post hoc features won't be available during inference in production and the model would perform badly.

## Dates
fastai library provides a utility function `add_datepart` to extract features from dates, such as is_year_end, dayOfWeek, etc. which are some semantic attributes in dates that we, humans, understand but not represented in date formats. 

## Categorical variables
Use pandas to specify categorical columns.

```python
sizes = 'Large','Large / Medium','Medium','Small','Mini','Compact'
df['ProductSize'] = df['ProductSize'].astype('category')
df['ProductSize'].cat.set_categories(sizes, ordered=True, inplace=True)
```

## Train/Validation split for time series data
It's crucial to know when it's good to randomly split a dataset into train and validation sets or not. For problems which prediction has a temporal aspect, the split must be done by time or ordering of data points. For example, in a investment forecasting problem, the validation set must cover completely different time range than training set. This is because the forecasting model will be used to predict values in future when used in production. And sometimes, the distribution shifts/varies over time and hence using the old data may not have any use while training our model. In this case, we may even benefit from discarding old data from training set.

## Extrapolation problem in trees
Since decision tree/random forest methods splits the data with the information in training set, they're incapable of extrapolation in regression problems.

## Embedding vs One-hot encoding
In neural networks, it's better to use embeddings over one-hot encodings for categorical variables, since embeddings capture semantics of categories. In one-hot encoding, there is no way to represent similarities or distances between categories.

## Out-of-distribution data points
We can train a model to predict whether a data point belongs to training set or validation set, to check whether there is any significant difference in distributions of them. If the model is successful to identify data points, then, it means training set and validation set are not similar in distribution. 

An alternative approach is to train separate models for train and validation dataset; then, compare feature importances.

## Inference confidence in random forests
In random forest, we can measure the confidence of prediction by variance of predictions made by estimators. If the variance is low, then, it means the estimators agree on this, hence, the random forest model is more confident.

## NNs vs Trees
Neural networks are more suitable than decision tree based methods when,
    - There are some high-cardinality categorical variables that are very important ("cardinality" refers to the number of discrete levels representing categories, so a high-cardinality categorical variable is something like a zip code, which can take on thousands of possible levels).
    - There are some columns that contain data that would be best understood with a neural network, such as plain text data.

## Feature similarity
```py
cluster_columns(xs)
```

## Partial dependence
```py
from sklearn.inspection import plot_partial_dependence

fig,ax = plt.subplots(figsize=(12, 4))
plot_partial_dependence(m, valid_xs_final, ['YearMade','ProductSize'], grid_resolution=20, ax=ax);
```