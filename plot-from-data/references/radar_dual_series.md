# Style: radar_dual_series

## Suitable Use Case

Radar/spider chart comparison between two methods across multiple benchmarks, emphasizing the advantage of the main method.

## Visual Features

- Font: `sans-serif` (DejaVu Sans / Arial), no LaTeX.
- Axis labels: about 9 pt, regular weight, multi-line text centered.
- Value labels: about 8 pt, same color as each series, with white-background bbox (`alpha=0.85`).
- Legend: outside the upper-left of the plot, black series names (main method bold), short colored line segments.
- Grid: concentric regular **octagonal** dashed grid. Use polygons with `close(angles)`, not circular approximation.
- Spine: `ax.set_frame_on(False)` to hide the polar axes outer frame.
- Fill transparency: `alpha=0.18` for both series.
- Linewidth ratio: main method about 2.8 pt, comparison method about 1.3 pt. The contrast is significant in the original figure.

## Color Example (DoRA Paper)

```python
C_DORA = '#76A676'  # pale gray-green
C_LORA = '#7D82FF'  # pale violet-blue
```

## Key Parameters

```python
fig, ax = plt.subplots(figsize=(8, 7.8), subplot_kw=dict(projection='polar'))
ax.set_theta_zero_location('N')    # 0 degrees at the top
ax.set_theta_direction(-1)         # clockwise
ax.set_yticks([]); ax.set_xticks([])

# Concentric regular octagonal grid (not circular!)
angles = np.linspace(0, 2*np.pi, N, endpoint=False)
for r in [0.4, 0.55, 0.7, 0.85, 1.0]:
    ax.plot(close(angles), close(np.full(N, r)),
            color='#CCCCCC', lw=0.8, linestyle='--')

# Data normalization: map each axis independently to [RMIN, RMAX]
RMIN, RMAX = 0.35, 1.0
def nrm(v, vmin, vmax): return RMIN + (RMAX-RMIN)*(v-vmin)/(vmax-vmin)

ax.fill(close(angles), close(dora_r), color=C_DORA, alpha=0.18)
ax.plot(close(angles), close(dora_r), color=C_DORA, lw=2.8)
ax.fill(close(angles), close(lora_r), color=C_LORA, alpha=0.18)
ax.plot(close(angles), close(lora_r), color=C_LORA, lw=1.3)

# Value labels with white background
ax.text(ang, r+0.08, f'{v:.2f}', ha='center', fontsize=7.8, color=C_DORA,
        bbox=dict(boxstyle='round,pad=0.12', facecolor='white',
                  edgecolor='none', alpha=0.85))

# Legend implemented with fig.text
fig.text(0.09, 0.90, '────  ', color=C_DORA, fontsize=12, fontweight='bold')
fig.text(0.155, 0.90, 'DoRA',  color='black',  fontsize=11, fontweight='bold')
```

## Reproduction Files

- `repro/radar_dora.py`
- `repro/radar_dora_repro.png`
