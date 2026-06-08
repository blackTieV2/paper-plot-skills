# Style: line_training_curve

## Suitable Use Case

Training-process curves showing convergence comparisons across multiple methods, with vertical breakpoint lines and a horizontal baseline/reference line.

## Visual Features

- Font: `sans-serif`, no LaTeX.
- Axis labels: about 12-13 pt, bold.
- Spine: all four sides visible.
- Ticks: outward (`direction='out'`).
- Grid: none.
- Legend: lower right, white background with gray frame.

## Color Example (AIME Training Curve)

```python
C_DYN   = '#5B0DAD'  # dark purple (main method)
C_NODYN = '#5BBCCA'  # soft cyan-green (comparison)
C_REF   = '#3D78C2'  # independent blue (horizontal reference line, distinct from main lines)
```

## Key Parameters

```python
# Horizontal reference line (independent color)
ax.axhline(ref_y, color=C_REF, lw=1.5, linestyle='--')

# Vertical breakpoint lines (matched to corresponding curve colors)
ax.axvline(step1, color=C_DYN,   lw=1.5, linestyle='--', alpha=0.85)
ax.axvline(step2, color=C_NODYN, lw=1.5, linestyle='--', alpha=0.85)

# Four-sided frame + outward ticks
for sp in ax.spines.values():
    sp.set_visible(True); sp.set_linewidth(1.0)
ax.tick_params(direction='out', length=4, width=0.8)
```

## Reproduction Files

- `repro/line_aime.py`
- `repro/line_aime_repro.png`
