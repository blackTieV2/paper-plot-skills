# Paper Plot Skills

This is a personal AI Skills toolkit for **reproducing and generating academic paper figures**.

I carefully selected charts from papers I have read whose visual styles are highly useful as references. These examples can greatly **reduce repetitive work when recreating paper-style plots**.

This repository is intended as a starting point. It extracts systematic style parameters from 9 real paper figures and supports two workflows: **fill a selected style with your own data** and **reproduce a figure from an image**.

These skills will continue to improve as you reproduce more figures.

If this is useful to you, please leave a star 🌟 to encourage continued improvement of this repository.

---

## 🎨 Preset Style Overview

| Style | Type | Source Paper | Key Features |
| ----------------------------------------------- | --- | ----------------- | -------------------------------- |
| `[bar_paired_delta](#bar_paired_delta)` | Bar chart | MemEvolve | Paired bars + gain arrows, serif font |
| `[bar_grouped_hatch](#bar_grouped_hatch)` | Bar chart | SPICE | Grouped bars + hatched main method, values above bars |
| `[line_confidence_band](#line_confidence_band)` | Line chart | Self-Distillation | EMA smoothing + confidence interval shading, LaTeX font |
| `[line_training_curve](#line_training_curve)` | Line chart | DAPO | Vertical breakpoint lines + horizontal reference line, sans-serif |
| `[line_loss_with_inset](#line_loss_with_inset)` | Line chart | SiameseNorm | L-shaped spine + axis-end arrows + right-side zoom inset |
| `[scatter_tsne_cluster](#scatter_tsne_cluster)` | Scatter plot | MemGen | t-SNE clusters + rounded colored annotation boxes, dotted grid |
| `[scatter_broken_axis](#scatter_broken_axis)` | Scatter plot | Meta-Harness | Broken x-axis dual panel, multiple marker types |
| `[radar_dual_series](#radar_dual_series)` | Radar chart | DoRA | Octagonal dashed concentric grid, two-method comparison |

---

## Skills

| Skill | Description | Trigger Example |
| --------------------------------------- | ------------------------------------- | ------------------------------- |
| **[plot-from-data](plot-from-data/)** | Choose any style above, fill in your data, and generate a dpi=300 paper-style figure | "Draw my data using the `bar_grouped_hatch` style" |
| **[plot-from-image](plot-from-image/)** | Upload a paper screenshot, automatically analyze proportions/fonts/colors, and reproduce it as a matplotlib script | "Help me reproduce this figure" |

---

## Original and Reproduction Overview

<table>
<tr>
<td align="center"><b>Figure Name</b></td>
<td align="center"><b>Original</b></td>
<td align="center"><b>Reproduction</b></td>
</tr>
<tr>
<td><code>bar_memevolve</code></td>
<td><img src="originals/bar_memevolve.png" width="260"></td>
<td><img src="repro/bar_memevolve_repro.png" width="260"></td>
</tr>
<tr>
<td><code>bar_spice</code></td>
<td><img src="originals/bar_spice.png" width="260"></td>
<td><img src="repro/bar_spice_repro.png" width="260"></td>
</tr>
<tr>
<td><code>line_selfdistill_train</code></td>
<td><img src="originals/line_selfdistill_train.png" width="260"></td>
<td><img src="repro/line_selfdistill_train_repro.png" width="260"></td>
</tr>
<tr>
<td><code>line_selfdistill_scale</code></td>
<td><img src="originals/line_selfdistill_scale.png" width="260"></td>
<td><img src="repro/line_selfdistill_scale_repro.png" width="260"></td>
</tr>
<tr>
<td><code>line_aime</code></td>
<td><img src="originals/line_aime.png" width="260"></td>
<td><img src="repro/line_aime_repro.png" width="260"></td>
</tr>
<tr>
<td><code>line_loss_inset</code></td>
<td><img src="originals/line_loss_inset.png" width="260"></td>
<td><img src="repro/line_loss_inset_repro.png" width="260"></td>
</tr>
<tr>
<td><code>scatter_tsne</code></td>
<td><img src="originals/scatter_tsne.png" width="260"></td>
<td><img src="repro/scatter_tsne_repro.png" width="260"></td>
</tr>
<tr>
<td><code>scatter_break</code></td>
<td><img src="originals/scatter_break.png" width="260"></td>
<td><img src="repro/scatter_break_repro.png" width="260"></td>
</tr>
<tr>
<td><code>radar_dora</code></td>
<td><img src="originals/radar_dora.png" width="260"></td>
<td><img src="repro/radar_dora_repro.png" width="260"></td>
</tr>
<tr>
<td><code>classwise_iou</code></td>
<td><img src="originals/classwise_iou.png" width="260"></td>
<td><img src="repro/classwise_iou_repro.png" width="260"></td>
</tr>
</table>

`classwise_iou` is an additional reproduction case produced directly through the `plot-from-image` workflow:

> Input image: [`originals/classwise_iou.png`](originals/classwise_iou.png)  
> Reproduction script: [`plot-from-image/scripts/classwise_iou_table.py`](plot-from-image/scripts/classwise_iou_table.py)

---

## Style Gallery

---

### Bar Charts

#### `bar_paired_delta` — Paired Gain Bars

> **Source**: MemEvolve: Meta-Evolution of Agent Memory Systems  
> Serif font, paired bars (baseline vs method), arrow-labeled gains, independent y-axis for each subplot  
> Parameter documentation: [`plot-from-data/references/bar_paired_delta.md`](plot-from-data/references/bar_paired_delta.md) · Script: [`plot-from-data/scripts/bar_memevolve.py`](plot-from-data/scripts/bar_memevolve.py)

<table><tr>
<td align="center"><b>Original</b></td>
<td align="center"><b>Reproduction</b></td>
</tr><tr>
<td><img src="originals/bar_memevolve.png" width="320"></td>
<td><img src="repro/bar_memevolve_repro.png" width="320"></td>
</tr></table>

---

#### `bar_grouped_hatch` — Grouped Bars with Hatch Fill

> **Source**: SPICE: Self-Play In Corpus Environments  
> LaTeX serif, grouped bars + white hatch fill on the main method, values above bars with best value bolded, open L-shaped spine  
> Parameter documentation: [`plot-from-data/references/bar_grouped_hatch.md`](plot-from-data/references/bar_grouped_hatch.md) · Script: [`plot-from-data/scripts/bar_spice.py`](plot-from-data/scripts/bar_spice.py)

<table><tr>
<td align="center"><b>Original</b></td>
<td align="center"><b>Reproduction</b></td>
</tr><tr>
<td><img src="originals/bar_spice.png" width="320"></td>
<td><img src="repro/bar_spice_repro.png" width="320"></td>
</tr></table>

---

### Line Charts

#### `line_confidence_band` — Confidence-Band Training Curve

> **Source**: Reinforcement Learning via Self-Distillation  
> LaTeX Computer Modern serif, EMA-smoothed main line, light confidence interval `fill_between`, bold SDPO legend  
> Parameter documentation: [`plot-from-data/references/line_confidence_band.md`](plot-from-data/references/line_confidence_band.md) · Script: [`plot-from-data/scripts/line_selfdistill.py`](plot-from-data/scripts/line_selfdistill.py)

<table><tr>
<td align="center"><b>Original</b></td>
<td align="center"><b>Reproduction</b></td>
</tr><tr>
<td><img src="originals/line_selfdistill_train.png" width="320"></td>
<td><img src="repro/line_selfdistill_train_repro.png" width="320"></td>
</tr></table>

---

#### `line_training_curve` — Vertical Breakpoints + Horizontal Reference Line

> **Source**: DAPO: An Open-Source LLM RL System at Scale  
> Sans-serif, four-sided frame, outward ticks, horizontal reference line in independent blue, two vertical dashed breakpoint lines matched to curve color  
> Parameter documentation: [`plot-from-data/references/line_training_curve.md`](plot-from-data/references/line_training_curve.md) · Script: [`plot-from-data/scripts/line_aime.py`](plot-from-data/scripts/line_aime.py)

<table><tr>
<td align="center"><b>Original</b></td>
<td align="center"><b>Reproduction</b></td>
</tr><tr>
<td><img src="originals/line_aime.png" width="320"></td>
<td><img src="repro/line_aime_repro.png" width="320"></td>
</tr></table>

---

#### `line_loss_with_inset` — L-Shaped Spine + Local Zoom Inset

> **Source**: SiameseNorm: Breaking the Barrier to Reconciling Pre/Post-Norm  
> LaTeX serif, L-shaped spine + axis-end arrows, dashed zoom box, black dashed connector to a separate right-side inset subplot  
> Parameter documentation: [`plot-from-data/references/line_loss_with_inset.md`](plot-from-data/references/line_loss_with_inset.md) · Script: [`plot-from-data/scripts/line_loss_inset.py`](plot-from-data/scripts/line_loss_inset.py)

<table><tr>
<td align="center"><b>Original</b></td>
<td align="center"><b>Reproduction</b></td>
</tr><tr>
<td><img src="originals/line_loss_inset.png" width="320"></td>
<td><img src="repro/line_loss_inset_repro.png" width="320"></td>
</tr></table>

---

### Scatter Plots

#### `scatter_tsne_cluster` — t-SNE Cluster Distribution

> **Source**: MemGen: Weaving Generative Latent Memory for Self-Evolving Agents  
> LaTeX serif, 7 clusters, rounded annotation boxes with uniform dark-gray edge and cluster-colored face, light-gray dotted grid, four-sided frame  
> Parameter documentation: [`plot-from-data/references/scatter_tsne_cluster.md`](plot-from-data/references/scatter_tsne_cluster.md) · Script: [`plot-from-data/scripts/scatter_tsne.py`](plot-from-data/scripts/scatter_tsne.py)

<table><tr>
<td align="center"><b>Original</b></td>
<td align="center"><b>Reproduction</b></td>
</tr><tr>
<td><img src="originals/scatter_tsne.png" width="320"></td>
<td><img src="repro/scatter_tsne_repro.png" width="320"></td>
</tr></table>

---

#### `scatter_broken_axis` — Broken X-Axis Scatter Plot

> **Source**: Meta-Harness: End-to-End Optimization of Model Harnesses  
> Bold sans-serif labels, dual-panel broken x-axis (0-50k | 115k/200k), multiple markers (★ ○ △ ◆ × ○), break marks only on the bottom edge  
> Parameter documentation: [`plot-from-data/references/scatter_broken_axis.md`](plot-from-data/references/scatter_broken_axis.md) · Script: [`plot-from-data/scripts/scatter_break.py`](plot-from-data/scripts/scatter_break.py)

<table><tr>
<td align="center"><b>Original</b></td>
<td align="center"><b>Reproduction</b></td>
</tr><tr>
<td><img src="originals/scatter_break.png" width="320"></td>
<td><img src="repro/scatter_break_repro.png" width="320"></td>
</tr></table>

---

### Radar Chart

#### `radar_dual_series` — Two-Method Multidimensional Comparison

> **Source**: DoRA: Weight-Decomposed Low-Rank Adaptation  
> Sans-serif, octagonal dashed concentric grid, thick dark-green DoRA line vs thin blue LoRA line, white-background value labels, legend in upper left  
> Parameter documentation: [`plot-from-data/references/radar_dual_series.md`](plot-from-data/references/radar_dual_series.md) · Script: [`plot-from-data/scripts/radar_dora.py`](plot-from-data/scripts/radar_dora.py)

<table><tr>
<td align="center"><b>Original</b></td>
<td align="center"><b>Reproduction</b></td>
</tr><tr>
<td><img src="originals/radar_dora.png" width="320"></td>
<td><img src="repro/radar_dora_repro.png" width="320"></td>
</tr></table>

---

### `plot-from-image` Example

#### `classwise_iou` — Class-Level Results Table

> **Source**: User-uploaded paper screenshot https://github.com/Trae1ounG/paper-plot-skills/issues/1 \
> Pure table-style layout, two result rows + strong/weak highlight background colors, reproduced directly according to the image's proportions and text layout  
> Input image: [`originals/classwise_iou.png`](originals/classwise_iou.png) · Script: [`plot-from-image/scripts/classwise_iou_table.py`](plot-from-image/scripts/classwise_iou_table.py)

<table><tr>
<td align="center"><b>Original</b></td>
<td align="center"><b>Reproduction</b></td>
</tr><tr>
<td><img src="originals/classwise_iou.png" width="320"></td>
<td><img src="repro/classwise_iou_repro.png" width="320"></td>
</tr></table>

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=Trae1ounG/paper-plot-skills&type=Date)](https://www.star-history.com/#Trae1ounG/paper-plot-skills&Date)
