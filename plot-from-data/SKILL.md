---
name: plot-from-data
description: |
  Generate publication-quality matplotlib figures by selecting a pre-built paper style and substituting user data.
  Use when: user provides data (numbers, arrays, or CSV) and wants a chart in a specific academic style;
  user asks to "plot this data", "make a bar chart", "draw a radar chart", "draw a chart in this style", "plot my data";
  or user selects a style name from the style catalog (bar_paired_delta, bar_grouped_hatch,
  line_confidence_band, line_training_curve, line_loss_with_inset, scatter_tsne_cluster,
  scatter_broken_axis, radar_dual_series).
---

# Plot From Data

Generate a paper-quality figure by picking a style template and filling it with user data. All outputs are `dpi=300` PNG.

## Available Styles

| Style | Type | Script | Suitable Use Case |
|-------|------|---------|-------------------|
| `bar_paired_delta` | Bar chart | `scripts/bar_memevolve.py` | Paired baseline vs method comparison with gain arrows |
| `bar_grouped_hatch` | Bar chart | `scripts/bar_spice.py` | Multi-method ablation, hatched main method, values above bars |
| `line_confidence_band` | Line chart | `scripts/line_selfdistill.py` | Training curve with confidence band |
| `line_training_curve` | Line chart | `scripts/line_aime.py` | Vertical breakpoint lines and horizontal reference line |
| `line_loss_with_inset` | Line chart | `scripts/line_loss_inset.py` | L-shaped spine with local zoom inset |
| `scatter_tsne_cluster` | Scatter plot | `scripts/scatter_tsne.py` | t-SNE clusters with annotation boxes |
| `scatter_broken_axis` | Scatter plot | `scripts/scatter_break.py` | Broken x-axis with multiple marker series |
| `radar_dual_series` | Radar chart | `scripts/radar_dora.py` | Two-method multidimensional comparison with octagonal grid |

## Workflow

```
1. Confirm the user's chart type and data.
2. Select the corresponding style. If unsure, ask the user or infer from the data shape.
3. Read references/<style_name>.md to obtain the exact parameters.
4. Copy the corresponding scripts/<script>.py file and replace the data section. The data section is clearly marked near the top of each script.
5. Run: python3 scripts/<script>.py
6. Check the output and fine-tune colors, labels, or font sizes if needed.
```

## Data Substitution Tips

Each reproduction script has a data section near the top, usually as `np.array(...)` or a dictionary. Replacement rules:

- Keep array dimensions and data types unchanged.
- If the number of categories changes, such as from 4 groups to 6 groups, update the color lists and width calculations accordingly.
- Modify x-axis labels and legend labels directly in the corresponding string lists.

## Detailed Style Parameters

Read the corresponding file in `references/` for exact `rcParams`, colors, font sizes, spine settings, and tick directions before generating:

- Bar: `references/bar_paired_delta.md`, `references/bar_grouped_hatch.md`
- Line: `references/line_confidence_band.md`, `references/line_training_curve.md`, `references/line_loss_with_inset.md`
- Scatter: `references/scatter_tsne_cluster.md`, `references/scatter_broken_axis.md`
- Radar: `references/radar_dual_series.md`
