## VAR-IRF

Impulse Response Function (IRF) utilities for VAR models with plotting helpers. Extracted from the workflow in `Tutorial.ipynb`.

### Installation

```bash
pip install var-irf
```

Repository: `https://github.com/TianzhuQin/Vector-Autoregression-Impulse-Response-Function`

Paper: [Hug fans or follow celebrities? How nationalism is reinforced on Chinese social media](https://www.science.org/doi/10.1126/sciadv.adu8241)

### Method summary (from the notebook)

- Fit a VAR(p) with `statsmodels.tsa.api.VAR(df).fit(lags)`.
- Get IRF object via `fit(...).irf(h)`:
  - IRF values: cumulative `cum_effects` (or non-cumulative `irfs`).
  - Error bands:
    - Asymptotic (`asym`): build ±z·stderr from covariance.
    - Monte Carlo (`mc`): direct lower/upper intervals.
- Plotting:
  - Central IRF curve, gradient shaded bands, style options.

### Quick start

```python
import pandas as pd
import matplotlib.pyplot as plt
from var_irf import compute_irf, plot_irf

# df is a DataFrame with multiple series columns and a time index
result = compute_irf(df, lags=2, horizon=7, stderr_type="asym", orth=False)

fig, ax = plt.subplots(figsize=(10, 8))
plot_irf(result, "Series1", "Series2", ax=ax, direction="single", band="shaded", layout="overlay", shaded=True)
ax.axhline(0, color='r', linestyle='dashdot', linewidth=0.5)
plt.show()
```

### API

- `compute_irf(df, lags=2, horizon=7, stderr_type='asym'|'mc', orth=False, cumulative=True, ...)`:
  Fit a VAR and return IRF arrays and error information.
- `plot_irf(result, impulse, response, ax=None, direction='single'|'bi', band='shaded'|'interval', layout='overlay'|'side-by-side', shaded=True, ...)`:
  Plot using the result from `compute_irf` with three orthogonal switches:
  - direction: single A→B or bidirectional.
  - band: shaded (gradient) or interval (errorbar-like); set `shaded=False` for line-only.
  - layout: overlay in one axes or side-by-side two subplots.

### License

MIT


### Citation

If you use this package in your research, please cite:

```bibtex
@article{
  HongKimZhangQin2025,
  author = {Hong, Ji Yeon and Kim, Yong H. and Zhang, Han and Qin, Tianzhu},
  title = {Hug fans or follow celebrities? How nationalism is reinforced on Chinese social media},
  journal = {Science Advances},
  year = {2025},
  volume = {11},
  number = {45},
  pages = {eadu8241},
  doi = {10.1126/sciadv.adu8241},
  url = {https://www.science.org/doi/10.1126/sciadv.adu8241}
}
```

