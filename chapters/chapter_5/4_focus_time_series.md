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

# Focus: Time Series

## ARIMA

```{code-cell}
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

import statsmodels.api as sm
import statsmodels.tsa.api as smts
import statsmodels.tsa.stattools as smtst

from statsmodels.tsa.statespace.sarimax import SARIMAX
from statsmodels.stats.diagnostic import acorr_ljungbox

from itertools import product
import tqdm
```

```{code-cell}
df = pd.read_csv('time_series.csv', index_col='Date', parse_dates=True)
df
```

```{code-cell}
def tsplot(y, lags=None, figsize=(20, 10), title=None):
    fig = plt.figure(figsize=figsize)

    layout = (2, 2)
    ts_ax = plt.subplot2grid(layout, (0, 0), colspan=2)
    acf_ax = plt.subplot2grid(layout, (1, 0))
    pacf_ax = plt.subplot2grid(layout, (1, 1))

    y.plot(ax=ts_ax)
    p_value = smts.adfuller(y)[1]
    if title is None:
        title = 'Time Series Analysis Plots'
    ts_ax.set_title('{0}\n Dickey-Fuller: p={1:.5f}'.format(title, p_value))
    
    smts.graphics.plot_acf(y, lags=lags, ax=acf_ax)
    smts.graphics.plot_pacf(y, lags=lags, ax=pacf_ax)
    plt.tight_layout()

tsplot(df, lags=60)
```

```{code-cell}
df_sdiff = (df - df.shift(7)).dropna()
tsplot(df_sdiff, lags=60)
```

```{code-cell}
df_2diff = df_sdiff.diff().dropna()
tsplot(df_2diff, lags=60)
```

```{code-cell}
candidate_model = sm.tsa.statespace.SARIMAX(df, order=(0, 1, 6), seasonal_order=(0, 1, 1, 7)).fit()
candidate_model.summary()
```

```{code-cell}
candidate_model.plot_diagnostics(figsize=(20,10))
plt.show()
```

```{code-cell}
lags = 60
fig, axes = plt.subplots(2, 1, figsize=(20, 10))
smts.graphics.plot_acf(candidate_model.resid, lags=lags, ax=axes[0])
smts.graphics.plot_pacf(candidate_model.resid, lags=lags, ax=axes[1])
plt.show()
```

```{code-cell}
acorr_ljungbox(candidate_model.resid, lags=[2*7], return_df=True, model_df=6)  # model_df = p + q
```

```{code-cell}
candidate_model2 = sm.tsa.statespace.SARIMAX(df, order=(0, 1, 4), seasonal_order=(0, 1, 1, 7)).fit()
candidate_model2.summary()
```

```{code-cell}
candidate_model2.plot_diagnostics(figsize=(20,10))
plt.show()
```

```{code-cell}
lags = 60
fig, axes = plt.subplots(2, 1, figsize=(20, 10))
smts.graphics.plot_acf(candidate_model2.resid, lags=lags, ax=axes[0])
smts.graphics.plot_pacf(candidate_model2.resid, lags=lags, ax=axes[1])
plt.show()
```

```{code-cell}
acorr_ljungbox(candidate_model.resid2, lags=[2*7], return_df=True, model_df=4)  # model_df = p + q
```


```{code-cell}
ps = range(0, 2)
qs = range(3, 6)

p = 0
d = 1 
q = 4

Ps = range(0, 2)
Qs = range(0, 3)

P = 0
D = 1 
Q = 1
s = 7

parameters = product(ps, qs, Ps, Qs)
parameters_list = list(parameters)
len(parameters_list)
```

```{code-cell}
def gs_arima(series, parameters_list, d, D, s, opt_method='powell'):

    results = []
    models = {}
    best_aic = float("inf")

    for param in parameters_list:
        # we need try-except because on some combinations model might fail to converge
        try:
            model = sm.tsa.statespace.SARIMAX(
                series, 
                order=(param[0], d, param[1]), 
                seasonal_order=(param[2], D, param[3], s)).fit(method=opt_method, disp=False)
        except:
            continue

        aic = model.aic
        if aic < best_aic:
            best_model = model
            best_aic = aic
            best_param = param
        results.append([param, model.aic])

    result_table = pd.DataFrame(results)
    result_table.columns = ['parameters', 'aic']
    result_table = result_table.sort_values(by='aic', ascending=True).reset_index(drop=True)
    
    return result_table, best_model

result_table, best_model = gs_arima(df, parameters_list, d, D, s)

result_table.head(10)
```

```{code-cell}
best_model.summary()
```

```{code-cell}
def mean_absolute_percentage_error(y_true, y_pred): 
    return np.mean(np.abs((y_true - y_pred) / y_true)) * 100

def plot_predictions(df, model, n_steps):
    """
        Plots model vs predicted values
        
        series - dataset with timeseries
        model - fitted model
        n_steps - number of steps to predict in the future
    """
    data = df.copy()
    data.columns = ['actual']
    data['arima_model'] = model.fittedvalues

    # forecast values
    data['arima_model'][:s+d] = np.NaN
    forecast = data['arima_model'].append(model.forecast(n_steps))

    # calculate error, again having shifted on s+d steps from the beginning
    error = mean_absolute_percentage_error(data['actual'][s+d:-n_steps], data['arima_model'][s+d:-n_steps])

    plt.figure(figsize=(20, 10))
    plt.title("Mean Absolute Percentage Error: {0:.2f}%".format(error))
    plt.plot(forecast, color='r', label="model")
    plt.axvspan(data.index[-1], forecast.index[-1], alpha=0.5, color='lightgrey')
    plt.plot(data.actual, label="actual", alpha=0.8)
    plt.legend()
    plt.grid(True)

plot_predictions(pd.DataFrame(series), best_model, 60)
```