# Style: bar_paired_delta (Paired Comparison Bars + Gain Labels)

**Source paper**: MemEvolve: Meta-Evolution of Agent Memory Systems  
**Chart type**: Grouped bar chart (2 bars per group: baseline vs method)  
**Reproduction code**: `repro/bar_memevolve.py`  
**Original image**: `image1.png`

---

## Visual Feature Description

- **Colors**: light steel blue `#A8C8E8` (baseline) + dark navy `#1B3D6E` (method), with strong cool-color contrast.
- **Gain labels**: red `#CC2200` bold percentage labels displayed above the method bars.
- **Arrows**: solid arrows from the baseline bar top to the method bar top.
- **Reference line**: black horizontal dashed line at the baseline height, spanning both bars.
- **Grid**: no grid.
- **Border**: solid border on all four sides, linewidth 1.4, slightly thick.
- **Axis labels**: bottom x-axis labels, no tick marks.
- **Title**: positioned inside the upper-left of the axes, with an emoji icon + bold title.
- **Overall style**: clean and contrast-focused, suitable for showing the absolute gain of a method relative to a baseline.

---

## Key Parameters

```python
COLOR_BASELINE = '#A8C8E8'
COLOR_METHOD   = '#1B3D6E'
COLOR_DELTA    = '#CC2200'

BAR_W   = 0.32
GAP     = 0.08          # spacing between the two bars
spine_linewidth = 1.4
grid    = False
title_position = 'upper left inside axes'
```

## Font & Bold Rules

| Element | Font Family | Font Size | Bold |
|------|--------|------|------|
| Subplot title (`"OWL-Workforce"`) | serif (Palatino / Times) | 11.5 | **Yes** |
| Red gain label (`"+7.1%"`) | serif (inherits global setting) | 9.5 | **Yes** |
| Y-axis label (`"Accuracy (Pass@1)"`) | serif (inherits global setting) | 10 | No |
| X-axis tick labels | serif (inherits global setting) | 10 | No |
| Y-axis tick numbers | serif (inherits global setting) | default | No |

```python
plt.rcParams.update({
    'font.family': 'serif',
    'font.serif': ['Palatino', 'Times New Roman', 'DejaVu Serif'],
})
```

> Note: the original figure title uses emoji icons (🦉🔷). Matplotlib serif fonts do not include emoji glyphs, so they may appear as small boxes. Replace them with text or use `AnnotationBbox` to insert icon images.

---

## Use Case

Applicable when the user has data in the following structure:

```
- Several groups (x-axis categories)
- Each group has two values: baseline and method
- The relative improvement percentage for each group needs to be highlighted
```

**Usage example (tell the agent this data format):**

```python
groups   = ['Web', 'xBench', 'TaskCraft', 'GAIA']
baseline = [58.1, 55.2, 58.7, 59.3]
method   = [62.3, 61.2, 65.5, 61.0]
delta    = ['+7.1%', '+10.9%', '+11.9%', '+2.7%']
title    = 'OWL-Workforce'
ylabel   = 'Accuracy (Pass@1)'
```

---

## Known Limitations

- The original title uses emoji icons (🦉🔷), but Matplotlib's default fonts do not support emoji rendering and may display empty boxes. Replace them with text or use `matplotlib.image` to place icon images.
- This style works best when value differences are in the 2%-20% range. If the gap is too large, the arrow proportions may look unbalanced.
