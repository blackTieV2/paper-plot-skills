# Style: scatter_tsne_cluster

## Suitable Use Case

Cluster visualization after reducing high-dimensional embeddings with t-SNE. Best for multi-class scatter plots with annotation boxes.

## Visual Features

- Font: serif + `usetex=True` (Computer Modern). If TeX is unavailable, use `STIX Two Text`.
- Title: two bold lines, about 13.5 pt.
- Axis labels: bold, about 12 pt.
- Ticks: regular weight, about 10 pt.
- Legend: upper right, white background with light-gray frame (`frameon=True, edgecolor='#CCCCCC'`), small markers.
- Points: `s=14, alpha=0.55`, no outline (`linewidths=0`), independent color for each cluster.
- Annotation boxes: `boxstyle='round,pad=0.30'`, unified dark-gray border (`#2C3E50`), background uses the corresponding cluster color with `alpha=0.28`.
- Grid: light-gray dotted grid (`linestyle=':', color='#E0E0E0', lw=0.6`).
- Spine: all four sides visible, dark gray (`#333333`), about 0.9 pt.
- Tick direction: inward (`direction='in'`).

## Color Example (MemEvolve Paper)

```python
DS_COLORS = {
    'GSM8K':    '#6A4C93',  # dark purple
    'MATH':     '#D651A0',  # magenta
    'GPQA':     '#F06292',  # rose pink
    'KodCode':  '#FF8A65',  # bright orange
    'BCB':      '#FFB74D',  # amber
    'ALFWorld': '#FFF176',  # bright yellow (easy to mistake for blue; be careful)
    'TriviaQA': '#C888E8',  # bright lavender purple
}
```

## Key Parameters

```python
plt.rcParams.update({
    'text.usetex': True,
    'font.family': 'serif',
    'font.serif': ['Computer Modern Roman', 'STIX Two Text'],
})

ax.scatter(x, y, c=color, s=14, alpha=0.55, linewidths=0, rasterized=True)

# Annotation box (cluster label)
import matplotlib.colors as mcolors
rgba = list(mcolors.to_rgba(color)); rgba[3] = 0.28
ax.annotate(r'\textbf{Name}', xy=...,
    bbox=dict(boxstyle='round,pad=0.30',
              facecolor=tuple(rgba),
              edgecolor='#2C3E50', linewidth=0.9))

# Legend
ax.legend(frameon=True, facecolor='white', edgecolor='#CCCCCC',
          markerscale=1.0, handlelength=0.8)

# Four-sided frame
for sp in ax.spines.values():
    sp.set_visible(True); sp.set_linewidth(0.9); sp.set_color('#333333')
ax.tick_params(direction='in', length=4, width=0.8)
ax.grid(True, color='#E0E0E0', linewidth=0.6, linestyle=':', zorder=0)
```

## Reproduction Files

- `repro/scatter_tsne.py`
- `repro/scatter_tsne_repro.png`
