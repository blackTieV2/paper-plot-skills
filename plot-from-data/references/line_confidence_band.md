# Style: line_confidence_band (Line Chart + Confidence Interval Shading)

**Source paper**: Reinforcement learning via self-distillation  
**Chart type**: Line chart (continuous training curve / discrete scaling curve) + semi-transparent confidence interval shading  
**Reproduction code**: `repro/line_selfdistill.py`  
**Original images**: `image2.png` (continuous), `image3.png` (discrete scaling)

---

## Visual Feature Description

- **Colors**: green `#3A8B3A` (main method SDPO) | blue `#3B6BB5` (comparison method GRPO) | gray `#999999` (base model).
- **Shading**: `fill_between` using the main line color with `alpha=0.15`; width represents the confidence interval.
- **Line width**: main method 1.8, secondary method 1.8, base model 1.4.
- **Markers** (scaling chart): filled circle `marker='o'`, size 6 pt.
- **Reference line** (training curve): horizontal gray dashed line `ls='--'` representing baseline performance.
- **Font**: LaTeX serif (`usetex=True`), title normal weight, main method bold in legend.
- **Spine**: only left/bottom visible (open style), linewidth 0.9, black.
- **Grid**: none.
- **Legend**: no border (`framealpha=0, edgecolor='none'`), positioned inside the plot.

---

## Key Parameters

```python
plt.rcParams.update({
    'text.usetex': True,
    'font.family': 'serif',
    'font.serif': ['Computer Modern Roman', 'STIX Two Text', 'DejaVu Serif'],
})

C_SDPO = '#3A8B3A'
C_GRPO = '#3B6BB5'
C_BASE = '#999999'

# Shading
ax.fill_between(x, mean - std, mean + std, color=C_SDPO, alpha=0.15)

# Line
ax.plot(x, mean, color=C_SDPO, lw=1.8, label=r'\textbf{SDPO}')

# Keep only left/bottom spines
for side, sp in ax.spines.items():
    sp.set_visible(side in ('left', 'bottom'))

# Borderless legend, bold main method
leg = ax.legend(framealpha=0, edgecolor='none')
for text in leg.get_texts():
    if 'main method name' in text.get_text():
        text.set_fontweight('bold')
```

---

## Two Subtypes

### Type A: Continuous Training Curve (`image2`)

- The x-axis is the step count, formatted as `0, 5k, 10k, 15k, 20k`.
- The shading narrows gradually during training (wide early, narrow later), simulated with `exp(-t)` decay.
- Legend is positioned in the **lower right**.
- Horizontal dashed reference line shows the performance level of the external baseline.

### Type B: Discrete Scaling Curve (`image3`)

- The x-axis is a discrete parameter scale; use evenly spaced `x_pos` plus manual tick labels to avoid log-axis distortion.
- Each data point has a circle marker.
- Legend is positioned in the **upper left**.
- No reference line.

---

## Use Case

Applicable when the user provides data in the following format:

```python
# Type A (training curve)
steps = np.linspace(0, 20000, 200)
sdpo_mean = [...]   # len=200
sdpo_std  = [...]   # len=200

# Type B (scaling curve)
param_labels = ['0.6B', '1.7B', '4B', '8B']
sdpo_pts = [0.215, 0.333, 0.450, 0.490]
sdpo_std = [0.005, 0.006, 0.008, 0.006]
```
