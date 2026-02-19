# Scientific Plotting Guidelines

> **Important:** A graph should be **self-explanatory**. Your reader should quickly grasp all key information without additional explanation.

---

## Tool Requirements

| Context | Tool | Notes |
|---------|------|-------|
| Paper submissions | **gnuplot** | Required for publications |
| Weekly meetings | Python/R/etc. | Acceptable, but follow the rules below |

---

## File Organization

Follow the structure used in [vtess/RTK](https://github.com/MoatLab/RTK):

```
project/
├── plot/      # Plotting scripts (.plot files)
├── dat/       # Data files
└── eps/       # Output graphs (.pdf, .eps)
```

**Workflow:** `gnuplot plot/my.plot` → check `eps/xxx.pdf`

---

## Labeling Requirements

Every graph **MUST** include:

| Element | Purpose |
|---------|---------|
| **X-axis label** | What the X values represent (with units) |
| **Y-axis label** | What the Y values represent (with units) |
| **Title** | What the result is about |
| **Legend** | What each line/bar represents |
| **Caption** | Key observations and takeaways |

### Scale Rules

| Rule | Why |
|------|-----|
| Y-axis starts from **ZERO** | Prevents misleading visualizations |
| Same scale for comparisons | Fair comparison between graphs |

---

## Readability Guidelines

| Aspect | Requirement |
|--------|-------------|
| **Font size** | Large fonts for all labels, legends |
| **Line width** | `lw 5` to `lw 20` in gnuplot |
| **Format** | Vector graphics only (`.pdf`, `.eps`) |
| **Colors** | Black, green, blue, red (distinguishable) |

### Avoid

| Don't | Why |
|-------|-----|
| `.jpg`, `.png` formats | Not scalable, pixelated when zoomed |
| Similar colors | Hard to distinguish |
| Small fonts | Unreadable in papers/presentations |

---

## Example

<img src="https://res.cloudinary.com/edwardedberg/image/upload/v1658335611/file-upload/cdf_merced_workload_jkjzob.jpg" alt="Example graph" width="600"/>

---

## References

- [Creating Decent Graphs (Swanson Lab)](https://swanson.ucsd.edu/2017/12/18/creating-decent-graphs/)
