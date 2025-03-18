# Interactive Plot of \( y(t) = e^{(a+ib)t} \)

```{code-cell} ipython3

import numpy as np
import matplotlib.pyplot as plt
import ipywidgets as widgets
from IPython.display import display

# Define the function y(t)
def compute_y(t, a, b):
    return np.exp((a + 1j * b) * t)

# Define the plotting function
def plot_function(a, b):
    t = np.linspace(0, 5, 500)
    y = compute_y(t, a, b)

    plt.figure(figsize=(8, 5))
    plt.plot(t, y.real, label="Real Part")
    plt.plot(t, y.imag, label="Imaginary Part", linestyle="dashed")
    plt.xlabel("t")
    plt.ylabel("y(t)")
    plt.title(r"$y(t) = e^{(a+ib)t}$")
    plt.legend()
    plt.grid(True)
    plt.show()

# Create static plot to check if Jupyter Book executes the notebook
plot_function(0.5, 1.0)  
```
