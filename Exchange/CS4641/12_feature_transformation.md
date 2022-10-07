# Feature Transformation

## Randomized projections
Works pretty well for classifications with small datasets with large numbers of features

## Principle Component Analysis
Singular value decomposition on dataset, that is find the ordered set of n-dimensional vectors that maximize the variation and where each vector is orthogonal to the prior vector.

TLDR: maximize correlation between features.

PCA Exercise:
- x = 2y, yes
- x = (2/3)y, no, still need extra one for 3rd col which is x = (5/6)y
- x = (1/2)y, no, need x = (1/3)y

Gives you global components. Has a notion of ordering

## Independent Component Analysis
All about probability and info theory. Can be thought of looking at local components. Is unordered.

## Comparison Discussion

| Clustering      | Feature Selection     | Feature Transformation |
| :------------- | :------------- | :--------------|
| small feature set|symbolic, better than f.t.|less information loss than f.s.|
|fixed K of groups|lots of noise|components|
|symbolic, better than F.T.|human-readable|data analysis|
|human-readable(-, not super human readable)||lots of features, not a lot of data|
