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

# Matplotlib

![](images/matplotlib.svg)

Matplotlib is a powerful Python library for creating a wide variety of data visualizations. Its key features include support for diverse plot types, extensive customization options, the ability to generate publication-quality graphics, extensibility, integration with NumPy, and interactive capabilities. It supports multiple output formats, has a large user community, and is open source. Matplotlib is an essential tool for data visualization and exploration.

```{code-cell}
import matplotlib.pyplot as plt
```

## Plot

```{code-cell}
import numpy as np

np.random.seed(0)
xpoints = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
ypoints = np.random.randint(-10, 30, size=len(xpoints))

plt.plot(xpoints, ypoints)
plt.show()
```