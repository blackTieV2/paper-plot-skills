# Style: scatter_broken_axis

## Suitable Use Case

Comparisons between low-context systems (0-50k) and high-context systems (115k, 200k), where the x-axis range is too uneven and needs a visual break.

## Visual Features

- Font: `sans-serif`, axis labels about 13 pt and bold.
- Spine: left panel uses an L-shaped spine (left + bottom); right panel keeps only the bottom spine.
- Break symbols: draw diagonal slashes only on the **bottom x-axis**; do not draw them at the top.
- Legend: lower right, white background with light-gray frame, 6 items in order.
- Scatter outlines: main series (Pareto stars, few-shot circles, etc.) use black outlines (`edgecolors='black', linewidths=0.8`).
- Non-Pareto points: no outline (`linewidths=0`) and lighter appearance (`alpha=0.85`).

## Color Example (Meta-Harness Paper)

```python
C_PARETO    = '#E53935'  # bright red
C_NONPARETO = '#F4B8B8'  # pale pink mist
C_DASH      = '#F0A0A0'  # pink dashed line
C_FEW       = '#6B4FA0'  # dark purple
C_FEW_LINE  = '#B8A8D8'  # light purple curve
C_MCE       = '#E69B00'  # orange
C_ACE       = '#2E86C1'  # blue
C_ZS        = '#5B2D8E'  # dark purple (zero-shot)
```

## Key Parameters

```python
# Dual-axis layout
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(9.5, 5.5),
    gridspec_kw={'width_ratios': [5, 1.3], 'wspace': 0.05})

# Break symbols (bottom edge only)
d = 0.015
kwargs = dict(transform=ax1.transAxes, color='k', clip_on=False, lw=1.2)
ax1.plot((1-d, 1+d), (-d, +d), **kwargs)   # bottom slash only
kwargs2 = dict(transform=ax2.transAxes, color='k', clip_on=False, lw=1.2)
ax2.plot((-d, +d), (-d, +d), **kwargs2)    # bottom slash

# L-shaped spine
ax1.spines['top'].set_visible(False)
ax1.spines['right'].set_visible(False)
ax2.spines[['top', 'right', 'left']].set_visible(False)

# Legend
from matplotlib.lines import Line2D
legend_elements = [
    Line2D([], [], marker='*', color='w', markerfacecolor=C_PARETO,
           markersize=11, label='Ours (Pareto)',
           linestyle='--', linewidth=1.2, markeredgecolor='black', markeredgewidth=0.8),
    ...
]
ax1.legend(handles=legend_elements, loc='lower right',
           frameon=True, facecolor='white', edgecolor='#CCCCCC')
```

## Reproduction Files

- `repro/scatter_break.py`
- `repro/scatter_break_repro.png`
