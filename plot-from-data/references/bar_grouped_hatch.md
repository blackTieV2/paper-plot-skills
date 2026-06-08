# Style: bar_grouped_hatch (Grouped Bars + Hatched Main Method)

**Source paper**: SPICE: Self-play in corpus environments improves reasoning  
**Chart type**: Grouped bar chart (3 bars per group, main method highlighted with hatch fill)  
**Reproduction code**: `repro/bar_spice.py`  
**Original image**: `image5.png`

---

## Visual Feature Description

- **Colors (ablation chart)**: light orange `#FFB695` / medium orange `#FF7F5E` / pure red `#D00000`, warm progressive palette.
- **Colors (comparison chart)**: light gray `#D3D3D3` / medium gray `#A9A9A9` / pure red `#D00000`. The medium gray should not be too dark (`#707070` is too dark and does not match the original grayscale).
- **Fill**: main method uses `//` hatch, with **white hatch lines carved over a dark red fill** (`hatch.color='white'`).
- **All bars** use unified `edgecolor='white'` to keep symmetric white gaps between bars. Hatch color is separately set to `white` through `rcParams['hatch.color']`.
- **Spine**: keep only left and bottom spines (open-axis style); hide top and right; line color `#333333`, linewidth 0.9.
- **Grid**: y-axis only, very light gray `#EBEBEB`, dashed `--`, linewidth 0.7.
- **Value labels**: display values above each bar. Main method labels are bold + dark red; other methods are regular black.
- **Grid**: light-gray horizontal y-axis lines only, `#DDDDDD`, placed behind the bars with low z-order.
- **Border**: keep all four borders visible, grayish `#7A7A7A`, linewidth 0.8, with the border layer above the bars.
- **Legend**: upper right, with border; swatches and hatch style match the bars.
- **Overall style**: academically clean, highlights the main method, suitable for ablation comparisons and multi-method comparisons.

---

## Key Parameters

```python
# Ablation chart colors
COLORS_ABL  = ['#F5C5A3', '#E8845A', '#C0392B']
# Comparison chart colors
COLORS_CMP  = ['#C8C8C8', '#707070', '#C0392B']

HATCHES     = ['', '', '//']          # Only the main method has hatch fill; // is sparser than //// and closer to the original
BEST_METHOD = 'SPICE'                 # This method's value labels are bold + red

bar_total_width = 0.78                # Total width of all bars in one group (about 78% of group width)
grid = 'y-only'                       # y-axis grid only
spine_all_visible = True              # Show all four borders
ymax = 85                             # Prevent bars from reaching too high
x_positions = [0.00, 1.23, 2.46, 3.69]
xlim = (-0.52, 4.18)                 # Left/right margins close to the original
legend_bbox = (0.992, 0.986)         # Legend box close to the upper right without touching the edge
```

## Font & Bold Rules

| Element | Font Family | Font Size | Bold |
|------|--------|------|------|
| Panel title (`"(a) SPICE Ablations"`) | LaTeX serif (Computer Modern style) | 13.2 | **No** (regular weight) |
| Legend text (non-main method) | LaTeX serif (Computer Modern style) | 9.2 | No |
| Legend text (main method `"SPICE"`) | LaTeX serif (Computer Modern style) | 9.2 | **Yes** |
| Value labels above bars (non-main method) | LaTeX serif (Computer Modern style) | 8.7 | No, black |
| Value labels above bars (main method) | LaTeX serif (Computer Modern style) | 8.7 | **Yes**, dark red `#8B0000` |
| Axis labels / ticks | LaTeX serif (Computer Modern style) | 10.8-11.2 | No |

```python
plt.rcParams.update({
    'text.usetex': True,
    'font.family': 'serif',
    'font.serif': ['Computer Modern Roman', 'STIX Two Text', 'DejaVu Serif'],
    'axes.unicode_minus': False,
})

# Bold the main method text separately in the legend
leg = ax.legend(...)
for text in leg.get_texts():
    if text.get_text() == BEST_METHOD:
        text.set_fontweight('bold')
```

---

## Use Case

Applicable to data with the following structure:

```
- Several benchmarks on the x-axis
- Each benchmark has comparison values for N methods (usually 2-4)
- One main method needs visual emphasis
- Two subplots: one ablation plot and one baseline comparison plot
```

**Usage example (tell the agent this data format):**

```python
benchmarks = ['MATH500', "AIME'25", 'GPQA-Diamond', 'MMLU-Pro']
data = {
    'Method A': [68.2,  6.7, 26.3, 51.6],
    'Method B': [72.6, 12.3, 31.8, 53.7],
    'SPICE':    [78.0, 19.1, 39.4, 58.1],   # Main method, automatically bold + hatched
}
best_method = 'SPICE'
title = '(a) SPICE Ablations'
ylabel = 'Accuracy (%)'
xlabel = 'Benchmark'
```

---

## Variant Suggestions

- Single-subplot version: call the `draw_panel` function directly and pass one data group.
- More than 3 methods: reduce `bar_total_width` appropriately to avoid bars becoming too thin.
- Main method not in the last column: adjust the `offset` calculation order.
- Do not rely only on coarse `loc='upper right'` legend control. Prefer `bbox_to_anchor` for pixel-level fine-tuning.
- The left and right subplots can each have their own `xlim / x_positions / legend_bbox`; do not force them to share one parameter set.
