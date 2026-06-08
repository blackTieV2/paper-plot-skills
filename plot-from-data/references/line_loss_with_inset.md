# Style: line_loss_with_inset

## Suitable Use Case

Training-loss curves where a local region needs to be enlarged to compare fine-grained differences, using an inset subplot for the zoomed area.

## Visual Features

- Font: serif + `usetex=True` (Computer Modern).
- Main plot: L-shaped spine (left + bottom only), **with axis-end arrows**.
- Inset: all four sides visible, relatively thick spine (1.2 pt).
- Connector line: black dashed line (`color='#333333', linestyle='--', lw=0.8`).
- Grid: light-gray dotted grid on the main plot (`linestyle=':', color='#E0E0E0'`); no grid in the inset.
- Legend: upper right of the main plot, white background with a very light gray frame.

## Color Example (SiameseNorm Paper, tab10 Palette)

```python
C_ORANGE = '#FF7F0E'  # HybridNorm (produces spike)
C_BLUE   = '#1F77B4'  # HybridNorm-ResiDual (high noise)
C_GREEN  = '#2CA02C'  # SiameseNorm Ours (smooth low loss)
```

## Key Parameters

```python
# Main plot L-shaped spine + axis-end arrows
ax_main.spines['top'].set_visible(False)
ax_main.spines['right'].set_visible(False)
# Axis-end arrows
ax_main.plot(1, 0, '>k', transform=ax_main.get_yaxis_transform(),
             clip_on=False, markersize=5)
ax_main.plot(0, 1, '^k', transform=ax_main.get_xaxis_transform(),
             clip_on=False, markersize=5)

# Local zoom box
zoom_rect = mpatches.FancyBboxPatch(
    (zoom_x1, zoom_y1), zoom_x2-zoom_x1, zoom_y2-zoom_y1,
    boxstyle='square,pad=0', linewidth=1.0, edgecolor='#333333',
    facecolor='none', linestyle='--', zorder=5)
ax_main.add_patch(zoom_rect)

# Connector line (from the right corner of the zoom box to the left side of the inset)
from matplotlib.patches import ConnectionPatch
con = ConnectionPatch(
    xyA=(zoom_x2, zoom_y2), coordsA=ax_main.transData,
    xyB=(ax_inset.get_xlim()[0], ax_inset.get_ylim()[1]),
    coordsB=ax_inset.transData,
    color='#333333', lw=0.8, linestyle='--')
fig.add_artist(con)

# Legend
ax_main.legend(loc='upper right', frameon=True,
               facecolor='white', edgecolor='#DDDDDD', framealpha=1.0)
```

## Notes

- The inset y-axis range should be determined jointly from the zoom box y-range and the blue-line peak. Do not set it too large, or the inset will contain excessive whitespace.
- The main plot y-axis should not start from 0. Start from the actual data minimum to match the original figure.

## Reproduction Files

- `repro/line_loss_inset.py`
- `repro/line_loss_inset_repro.png`
