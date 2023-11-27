---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Scikit-Learn

![](images/scikit-learn.png)

Scikit-learn is a machine learning library in Python that provides simple and efficient tools for data analysis and modeling. It includes various modules for tasks such as regression, classification, clustering, dimensionality reduction, and model selection. The library emphasizes ease of use, high performance, and an extensive set of algorithms, making it a popular choice for both beginners and experienced practitioners in the field of machine learning.

```{code-cell}
import sklearn
```

```{code-cell}
import numpy as np
import pandas as pd

np.random.seed(0)

data = pd.DataFrame({
    'Target': np.random.normal(100, 10, 10),
    'X1': np.random.normal(0, 5, 10),
    'X2': np.random.uniform(0, 100, 10),
    'X3': np.random.choice(['A', 'B'], 10),
    'X4': np.random.choice(['X', 'Y', 'Z'], 10),
    'X5': np.random.choice(['low', 'medium', 'high'], 10)
})

data.loc[[2, 5, 8], 'X1'] = np.nan
data.loc[[3, 6, 8], 'X2'] = np.nan

data
```

## Pre-Processing

Scikit-learn provides a comprehensive suite of preprocessing tools, including feature scaling, normalization, encoding of categorical variables, handling of missing data, and transformation of data into a suitable format for model training. These preprocessing steps are crucial for improving the performance and reliability of machine learning models by ensuring that the input data is appropriately formatted and scaled for the algorithms being employed.

### Missing Data
```{code-cell}
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(strategy='mean')
data[['X1', 'X2']] = imputer.fit_transform(data[['X1', 'X2']])

data
```

### Scaling

**Standardization**
```{code-cell}
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
data[['X1', 'X2']] = scaler.fit_transform(data[['X1', 'X2']])

data
```

**Normalization**
```{code-cell}
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
data[['X1', 'X2']] = scaler.fit_transform(data[['X1', 'X2']])

data
```


### Encoding

**Binarization**
```{code-cell}
from sklearn.preprocessing import Binarizer

binarizer = Binarizer(threshold=0.5)
data[['X1', 'X2']] = binarizer.transform(data[['X1', 'X2']])

data
```

**One-Hot**
```{code-cell}
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(sparse_output=False, drop='first')
data_encoded = pd.DataFrame(encoder.fit_transform(data[['X3', 'X4']]),
                            columns=encoder.get_feature_names_out(['X3', 'X4']))

data = pd.concat([data.drop(columns=['X3', 'X4']), data_encoded], axis=1)

data
```

**Ordinal Encoder**
```{code-cell}
from sklearn.preprocessing import OrdinalEncoder

encoder = OrdinalEncoder(categories=[['low', 'medium', 'high']])
data['X5'] = encoder.fit_transform(data['X5'].values.reshape(-1, 1))

data
```

### Train-Test Split
```{code-cell}
from sklearn.model_selection import train_test_split

X = data.drop('Target', axis=1)
y = data['Target']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```


## Model Development & Predictions

**Regression**

| Model | Module |
| :---: | :----: |
| Linear | `from sklearn.linear_model import LinearRegression` |
| Poisson | `from sklearn.linear_model import PoissonRegressor` |
| Gamma | `from sklearn.linear_model import GammaRegressor` |
| Ridge | `from sklearn.linear_model import Ridge` |
| Lasso | `from sklearn.linear_model import Lasso` |
| Elastic Net | `from sklearn.linear_model import ElasticNet` |
| K-Nearest Neighbors Regression (KNN) | `from sklearn.neighbors import KNeighborsRegressor` |
| Support Vector Regression (SVR) | `from sklearn.svm import SVR` |
| Decision Tree Regression | `from sklearn.tree import DecisionTreeRegressor` |
| Random Forest | `from sklearn.ensemble import RandomForestRegressor` |
| Ada-Boost | `from sklearn.ensemble import AdaBoostRegressor` |
| XG-Boost | `from xgboost import XGBRegressor` |


**Classification**

| Model | Module |
| :---: | :----: |
| Logistic Regression | `from sklearn.linear_model import LogisticRegression` |
| Binary Naive Bayes | `from sklearn.naive_bayes import BernoulliNB` |
| Multinomial Naive Bayes | `from sklearn.naive_bayes import MultinomialNB` |
| Ridge | `from sklearn.linear_model import RidgeClassifier` |
| Lasso | `from sklearn.linear_model import LogisticRegression` with `penalty='l1', solver='liblinear'` |
| ElasticNet | `from sklearn.linear_model import LogisticRegression` with `penalty='elasticnet', solver='saga', l1_ratio=0.5` |
| K-Nearest Neighbors (KNN) | `from sklearn.neighbors import KNeighborsClassifier` |
| Support Vector Machine (SVM) | `from sklearn.svm import SVC` |
| Decision Tree | `from sklearn.tree import DecisionTreeClassifier` |
| Random Forest | `from sklearn.ensemble import RandomForestClassifier` |
| Ada-Boost | `from sklearn.ensemble import AdaBoostClassifier` |
| XG-Boost | `from xgboost import XGBClassifier` |


**Clustering**

| Model | Module |
| :---: | :----: |
| Agglomerative Hierarchical Clustering | `from sklearn.cluster import AgglomerativeClustering` |
| K-Means | `from sklearn.cluster import KMeans` |
| Gaussian Mixture Model (GMM) | `from sklearn.mixture import GaussianMixture` |
| DBSCAN | `from sklearn.cluster import DBSCAN` |


**Dimensionality Reduction**

| Model | Module |
| :---: | :----: |
| Principal Component Analysis (PCA) | `from sklearn.decomposition import PCA` |
| Factor Analysis | `from sklearn.decomposition import FactorAnalysis` |
| t-SNE | `from sklearn.manifold import TSNE` |
| Truncated SVD | `from sklearn.decomposition import TruncatedSVD` |


```{code-cell}
from sklearn.neighbors import KNeighborsRegressor

model = KNeighborsRegressor(n_neighbors=5)
model.fit(X_train, y_train)

y_pred = model.predict(X_test)
```

## Model  Evaluation

**Regression**

| Metric | Module |
| :----: | :----: |
| Mean Squared Error (MSE) | `from sklearn.metrics import mean_squared_error` |
| Mean Absolute Error (MAE) | `from sklearn.metrics import mean_absolute_error` |
| Coefficient of Determination (R²) | `from sklearn.metrics import r2_score` |


**Classification**

| Metric | Module |
| :----: | :----: |
| Accuracy | `from sklearn.metrics import accuracy_score` |
| Precision | `from sklearn.metrics import precision_score` |
| Recall | `from sklearn.metrics import recall_score` |
| F1-Score | `from sklearn.metrics import f1_score` |
| Classification Report | `from sklearn.metrics import classification_report` |
| Confusion Matrix | `from sklearn.metrics import confusion_matrix` |
| AUC & ROC | `from sklearn.metrics import roc_auc_score` |


**Clustering**

| Metric | Module |
| :----: | :----: |
| Adjusted Rand Index (ARI) | `from sklearn.metrics import adjusted_rand_score` |
| Homogeneity Score | `from sklearn.metrics import homogeneity_score` |
| Silhouette Score | `from sklearn.metrics import silhouette_score` |

```{code-cell}
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score

mse = mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)
mae = mean_absolute_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print(f'Mean Squared Error (MSE): {round(mse, 2)}')
print(f'Root Mean Squared Error (RMSE): {round(rmse, 2)}')
print(f'Mean Absolute Error (MAE): {round(mae, 2)}')
print(f'R-squared: {round(r2, 3)}')
```

```{code-cell}
from sklearn.model_selection import cross_val_score

y_train_pred = model.predict(X_train)
mse_train = mean_squared_error(y_train, y_train_pred)

cv_scores = cross_val_score(model, X, y, cv=5, scoring='neg_mean_squared_error')
cv_mse = -cv_scores

print(f'Train MSE: {round(mse_train, 2)}')
print(f'Cross-Validation MSE: {round(cv_mse.mean(), 2)}')
print(f'Test MSE: {round(mse, 2)}')
```


## Model Tuning

```{code-cell}
from sklearn.model_selection import GridSearchCV

param_grid = {
    'n_neighbors': [2, 3, 4, 5],
    'weights': ['uniform', 'distance'],
    'metric': ['euclidean', 'manhattan']
}

grid_search = GridSearchCV(model, param_grid, cv=5, scoring='neg_mean_squared_error')
grid_search.fit(X_train, y_train)
print("Migliori parametri:", grid_search.best_params_)

y_train_pred = best_model.predict(X_train)
mse_train = mean_squared_error(y_train, y_train_pred)

best_model = grid_search.best_estimator_
cv_scores = cross_val_score(best_model, X_train, y_train, cv=5, scoring='neg_mean_squared_error')
cv_mse = -cv_scores

y_pred = grid_search.predict(X_test)
mse = mean_squared_error(y_test, y_pred)

print(f'Train MSE: {round(mse_train, 2)}')
print(f'Cross-Validation MSE: {round(cv_mse.mean(), 2)}')
print(f'Test MSE: {round(mse, 2)}')
```

```{code-cell}
from sklearn.model_selection import RandomizedSearchCV

param_dist = {
    'n_neighbors': [2, 3, 4, 5],
    'weights': ['uniform', 'distance'],
    'metric': ['euclidean', 'manhattan']
}

random_search = RandomizedSearchCV(model, param_distributions=param_dist, n_iter=10, cv=5, scoring='neg_mean_squared_error', random_state=0)
random_search.fit(X_train, y_train)
print("Best parameters:", random_search.best_params_)

y_train_pred = best_model.predict(X_train)
mse_train = mean_squared_error(y_train, y_train_pred)

best_model = grid_search.best_estimator_
cv_scores = cross_val_score(best_model, X_train, y_train, cv=5, scoring='neg_mean_squared_error')
cv_mse = -cv_scores

y_pred = grid_search.predict(X_test)
mse = mean_squared_error(y_test, y_pred)

print(f'Train MSE: {round(mse_train, 2)}')
print(f'Cross-Validation MSE: {round(cv_mse.mean(), 2)}')
print(f'Test MSE: {round(mse, 2)}')
```
