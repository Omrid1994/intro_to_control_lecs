---
title: Interactive Plot of $y(t) = e^{a_1 + i b_1} + e^{a_2 + i b_2}$
---

# Interactive Visualization

This interactive plot allows you to modify the values of $a_1, b_1, a_2, b_2$ using sliders. The function being visualized is:

```{math}
y(t) = e^{a_1 + i b_1} + e^{a_2 + i b_2}
```

## **Interactive Plot Implementation**

```{code-cell}
import numpy as np
import matplotlib.pyplot as plt
import ipywidgets as widgets
from ipywidgets import interactive

def plot_y(a1=0, b1=0, a2=0, b2=0):
    t = np.linspace(-5, 5, 1000)
    y_t = np.exp(a1 + 1j * b1) + np.exp(a2 + 1j * b2)

    plt.figure(figsize=(8, 4))
    plt.plot(t, np.real(y_t) * np.ones_like(t), label="Re(y(t))", color='blue')
    plt.plot(t, np.imag(y_t) * np.ones_like(t), label="Im(y(t))", color='red')

    plt.axhline(0, color="black", linewidth=0.5)
    plt.axvline(0, color="black", linewidth=0.5)

    plt.xlabel("t")
    plt.ylabel("y(t)")
    plt.title(r"$y(t) = e^{a_1 + i b_1} + e^{a_2 + i b_2}$")
    plt.legend()
    plt.grid(True)
    plt.show()

widget = interactive(plot_y, 
                     a1=widgets.FloatSlider(min=-5, max=5, step=0.1, value=0, description="a1"),
                     b1=widgets.FloatSlider(min=-5, max=5, step=0.1, value=0, description="b1"),
                     a2=widgets.FloatSlider(min=-5, max=5, step=0.1, value=0, description="a2"),
                     b2=widgets.FloatSlider(min=-5, max=5, step=0.1, value=0, description="b2"))

display(widget)
```

## **How to Use**
- Adjust the sliders for $a_1, b_1, a_2, b_2$.
- Observe how the real and imaginary parts of $y(t)$ change.
- The plot updates dynamically in the Jupyter Book HTML output.