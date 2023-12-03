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

# Statsmodels

![](images/statsmodels.png)

Statsmodels provides statistical models and tools for data analysis. It is designed to support the estimation and testing of statistical models in various contexts, including econometrics, linear and non-linear regression, time series analysis, and more. The library is divided into different modules that cover a wide range of statistical techniques and allows users to perform hypothesis testing, statistical modeling, and exploration of relationships within datasets. 

```{code-cell}
import statsmodels.api as sm
```

```{code-cell}
import numpy as np
import pandas as pd

np.random.seed(0)

data = pd.DataFrame({
    'Target': np.random.normal(100, 10, 10),
    'X1': np.random.normal(0, 5, 10),
    'X2': np.random.uniform(0, 100, 10),
    'X3': np.random.choice(['A', 'B'], 10)
})

data = pd.get_dummies(data, columns=['X3'], drop_first=True)
data['X3_B'] = data['X3_B'].astype(float)

data
```

## Regression & Classification

| Model | Function |
| :---: | :------: |
| Linear | `sm.OLS` |
| Logit | `sm.Logit` |
| Poisson | `sm.GLM` with `family=sm.families.Poisson()` |
| Gamma | `sm.GLM` with `family=sm.families.Gamma()` |
| Negative Binomial | `sm.GLM` with `family=sm.families.NegativeBinomial()` |
| Zero-Inflated Poisson | `ZeroInflatedPoisson` |
| Zero-Inflated Negative Binomial | `ZeroInflatedNegativeBinomial` |
| Robust Regression | `sm.RLM` |
| Quantile Regression | `sm.QuantReg` |


```{code-cell}
model = sm.OLS(data['Target'], data[['X1', 'X2', 'X3_B']])
results = model.fit()

results.summary()
```


## ANOVA & ANCOVA

**ANOVA**
```{code-cell}
from statsmodels.formula.api import ols

model = ols('Target ~ X3_B', data=data)
results = model.fit()

anova_table = sm.stats.anova_lm(results, typ=2)
anova_table
```

**ANCOVA**
```{code-cell}
from statsmodels.formula.api import ols

model = ols('Target ~ X3_B + X1', data=data)
results = model.fit()

anova_table = sm.stats.anova_lm(results, typ=2)
anova_table
```


## Time Series

```{code-cell}
t = np.arange(100)
trend = 0.5 * t
season = 10 * np.sin(2 * np.pi * t / 12)
noise = np.random.normal(0, 1, 100)

y = trend + noise
y_season = trend + season + noise
x = 5 * np.sin(2 * np.pi * t)

data = pd.DataFrame({'Time': t, 'Value': y, 'Value_Season': y_season, 'Exo_Var': x})
data
```

### ARIMA

```{code-cell}
from statsmodels.tsa.arima.model import ARIMA

model = ARIMA(data['Value'], order=(1, 1, 1))
results = model.fit()

results.summary()
```

### SARIMA

```{code-cell}
from statsmodels.tsa.statespace.sarimax import SARIMAX

model = SARIMAX(data['Value_Season'], order=(1, 1, 1), seasonal_order=(1, 1, 1, 12))
results = model.fit()

results.summary()
```

### ARIMAX & SARIMAX

```{code-cell}
model = ARIMA(data['Value'], order=(1, 1, 1), exog=data[['Exo_Var']])
# model = SARIMAX(data['Value_Season'], order=(1, 1, 1), seasonal_order=(1, 1, 1, 12))
results = model.fit()

results.summary()
```

### VAR

```{code-cell}
from statsmodels.tsa.api import VAR

var_data = data[['Value', 'Exo_Var']]
model = VAR(var_data)
results = model.fit()

results.summary()
```


## Panel Data


## Tests

| Category | Type | Function |
| :------: | :--: | :------: | 
| ANOVA & ANCOVA    |                        | `sm.stats.anova_lm`         |
| Autocorrelation   | Ljung-Box              | `sm.stats.diagnostic.acorr_ljungbox` |
| Homoschedasticity | Breusch–Pagan          | `sm.stats.het_breuschpagan` |
|                   | White                  | `sm.stats.het_white`        |
| Normality         | D'Agostino-Pearson     | `sm.stats.normaltest`       |
|                   | Kolmogorov-Smirnov     | `sm.stats.kstest`           |
|                   | Shapiro-Wilk           | `sm.stats.shapiro`          |
| Parameter Values  | Likelihood Ratio       | `compare_lr_test`           |
|                   | Lagrange Multipliers   | `score_test`                |
|                   | Wald                   | `wald_test`                 |
| Seasonality       | Kwiatkowski-Phillips-Schmidt-Shin (KPSS) | `sm.tsa.kpss` |
| Stationarity      | Dickey-Fuller (ADF)    | `sm.tsa.stattools.adfuller` |
| Time Series Causality | Granger            | `sm.tsa.stattools.grangercausalitytests` |

