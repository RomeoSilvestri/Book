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

![](images/statsmodeld.png)

Statsmodels provides statistical models and tools for data analysis. It is designed to support the estimation and testing of statistical models in various contexts, including econometrics, linear and non-linear regression, time series analysis, and more. The library is divided into different modules that cover a wide range of statistical techniques and allows users to perform hypothesis testing, statistical modeling, and exploration of relationships within datasets. 

```{code-cell}
import statsmodels.api as sm
```

## Tests

**ANOVA test**

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


## ANOVA & ANCOVA

**ANOVA**
```{code-cell}
from statsmodels.formula.api import ols

model = ols( ~ , data=data)
model.fit()
model.summary()
```

**ANCOVA**
cambia solo in ols
```{code-cell}
from statsmodels.formula.api import ols

model = ols( ~ , data=data)
model.fit()
model.summary()
```

## Time Series

### ARIMA
### SARIMA
### VAR


## Panel Data


