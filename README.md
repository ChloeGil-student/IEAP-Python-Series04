# IEAP-Python-Series04

Preparatory assignment **pre-Series 04 – Python** of the Master IEAP (University of Montpellier).
Starting from a known 3D sinusoidal signal, we estimate its time derivative with finite differences, compute its tangential speed in any number of dimensions (with tested functions), and plot it interactively with Plotly.

## Group

| Member | GitHub branch | Work section |
|---|---|---|
| GILLES Chloé | `Chloe` | 1. Generate a known signal; 2. Estimate the time derivative of the signal |
| DELFIN Elouan | `Elouan-branch` | 3. Estimate the tangential speed of the signal |
| WAHEED Ayesha | `Ayesha` | 4. Create an interactive plot with the plotly library |


## Repository content

| File | Description |
|---|---|
| `Series04 Python.ipynb` | Main notebook: math (LaTeX), code, plots and tests |
| `references.bib` | BibTeX entries for every reference cited in the notebook |
| `LICENSE` | MIT License |
| `README.md` | This file |

## Notebook outline

1. **Generate a known signal**
   - Equation of a 1 Hz sinusoid, amplitude 1, phase 0: $s(t)=\sin(2\pi t)$.
   - Time vector as a column vector `(n, 1)`, signal as a `(n, 3)` array (x, y, z over columns), with a $\pi/4$ phase shift from x to y and from y to z (NumPy broadcasting).
   - 2D (amplitude vs. time) and 3D (x, y, z) plots with Matplotlib.

2. **Estimate the time derivative of the signal**
   - Derivative of a sine wave from Euler's formulas [1]: $\frac{d}{dt}A\sin(2\pi f t+\varphi)=2\pi f A\cos(2\pi f t+\varphi)$, written for each axis.
   - Forward vs. central difference [2]: accuracy ($O(h)$ vs. $O(h^2)$), time localisation, edge handling, noise.
   - Two functions, `forward_difference(signal, time)` and `central_difference(signal, time)`, returning an `(n, d)` array (same shape as the signal; borders completed with one-sided differences).
   - Overlay plots of the signal and its estimated derivative.

3. **Estimate the tangential speed of the signal**
   - Tangential velocity (vector) vs. tangential speed (scalar, norm of the velocity) [3, 4].
   - Formula in 3D, $v=\sqrt{\dot x^2+\dot y^2+\dot z^2}$, and in nD, $v=\lVert\dot{\vec r}\rVert_2=\sqrt{\sum_k \dot x_k^2}$.
   - `tangential_speed(signal, time)`: central difference followed by the Euclidean norm across columns; returns an `(n, 1)` array.
   - Test cell with `assert` statements, each expected value derived by hand first: 1D (uniform, backwards, accelerated), 2D circle, 3D line and helix, 4D and 6D lines, no movement, non-uniform sampling, output shape for $d = 1, 2, 3, 4, 7$, non-negative speed.

4. **Interactive plot with Plotly**
   - Signal and tangential speed in a zoomable Plotly figure, kept interactive in the exported HTML file.

### Function conventions

All functions take their inputs in the order **`(signal, time)`**: the data first, then the coordinate along which we differentiate, as in `np.gradient(f, x)` or `np.trapz(y, x)`. Samples are always over rows:

| Function | `signal` | `time` | Output |
|---|---|---|---|
| `forward_difference` | `(n, d)` | `(n, 1)` or `(n,)` | `(n, d)` |
| `central_difference` | `(n, d)` | `(n, 1)` or `(n,)` | `(n, d)` |
| `tangential_speed` | `(n, d)` or `(n,)` | `(n, 1)` or `(n,)` | `(n, 1)` |

## How to run

Requirements: Python 3, `numpy`, `matplotlib`, `plotly`, and Jupyter.

```bash
git clone https://github.com/ChloeGil-student/IEAP-Python-Series04.git
cd IEAP-Python-Series04
pip install numpy matplotlib plotly jupyter
jupyter notebook "Series04 Python.ipynb"
```

Run all cells from top to bottom: the test cell prints `All tangential speed tests passed.` when every assertion holds.

## References

The full BibTeX entries are in [`references.bib`](references.bib). Numbers match the citations in the notebook.

1. E. Le Clézio, *Mathematics Prolegomena*, Master IEAP, University of Montpellier, September 2025.
2. Wikipedia, *Finite difference* (forward, backward, central): <https://en.wikipedia.org/wiki/Finite_difference>
3. Wikipedia, *Speed* (speed = magnitude of the velocity vector): <https://en.wikipedia.org/wiki/Speed>
4. Wikipedia, *Tangential speed* (tangential speed vs. tangential velocity): <https://en.wikipedia.org/wiki/Tangential_speed>
5. Plotly, *Plotly Open Source Graphing Library for Python:* <https://plotly.com/python/>

## License

Released under the [MIT License](LICENSE) © 2026 DELFIN Elouan, WAHEED Ayesha, GILLES Chloé.
