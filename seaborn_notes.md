# 📊 Complete Seaborn Course: Mastering Data Visualization in Python

> A comprehensive guide covering every major plot type in Seaborn — from figure-level to axis-level functions — with definitions, real-world use cases, code examples, and customization arguments.

---

## Table of Contents

1. [Introduction to Seaborn](#1-introduction-to-seaborn)
2. [Figure-Level vs Axes-Level Functions](#2-figure-level-vs-axes-level-functions)
3. [Figure-Level Functions](#3-figure-level-functions)
   - [relplot()](#31-relplot)
   - [displot()](#32-displot)
   - [catplot()](#33-catplot)
4. [Relational Plots (Axes-Level)](#4-relational-plots-axes-level)
   - [scatterplot()](#41-scatterplot)
   - [lineplot()](#42-lineplot)
5. [Distribution Plots (Axes-Level)](#5-distribution-plots-axes-level)
   - [histplot()](#51-histplot)
   - [kdeplot()](#52-kdeplot)
   - [ecdfplot()](#53-ecdfplot)
   - [rugplot()](#54-rugplot)
6. [Categorical Plots (Axes-Level)](#6-categorical-plots-axes-level)
   - [barplot()](#61-barplot)
   - [countplot()](#62-countplot)
   - [boxplot()](#63-boxplot)
   - [violinplot()](#64-violinplot)
   - [stripplot()](#65-stripplot)
   - [swarmplot()](#66-swarmplot)
   - [pointplot()](#67-pointplot)
   - [boxenplot()](#68-boxenplot)
7. [Matrix / Heatmap Plots](#7-matrix--heatmap-plots)
   - [heatmap()](#71-heatmap)
   - [clustermap()](#72-clustermap)
8. [Regression Plots](#8-regression-plots)
   - [lmplot()](#81-lmplot)
   - [regplot()](#82-regplot)
   - [residplot()](#83-residplot)
9. [Multi-Plot Grids](#9-multi-plot-grids)
   - [pairplot()](#91-pairplot)
   - [FacetGrid](#92-facetgrid)
   - [PairGrid](#93-pairgrid)
10. [Themes and Aesthetics](#10-themes-and-aesthetics)
11. [Color Palettes](#11-color-palettes)
12. [Quick Reference Cheat Sheet](#12-quick-reference-cheat-sheet)

---

## 1. Introduction to Seaborn

Seaborn is a Python data visualization library built on top of Matplotlib. It provides a high-level interface for drawing attractive and informative statistical graphics. Seaborn integrates tightly with Pandas DataFrames, making it extremely practical for exploratory data analysis (EDA).

### Why Seaborn?

- Built-in statistical estimation (mean, CI, regression lines)
- Beautiful default themes
- Direct Pandas DataFrame support
- Concise API compared to raw Matplotlib

### Installation

```python
pip install seaborn
```

### Basic Imports

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# Load a built-in dataset for examples
tips = sns.load_dataset("tips")
penguins = sns.load_dataset("penguins")
flights = sns.load_dataset("flights")
iris = sns.load_dataset("iris")
```

---

## 2. Figure-Level vs Axes-Level Functions

This is the most important concept to understand before diving into the plots.

### Axes-Level Functions

- Draw onto a single `matplotlib.pyplot.Axes` object
- Can be embedded into larger matplotlib figures
- Accept an `ax=` argument to target a specific subplot
- Return a matplotlib `Axes` object

### Figure-Level Functions

- Manage their own matplotlib `Figure` via a `FacetGrid`
- Support faceting (splitting data into multiple subplots by a variable)
- Have `height` and `aspect` parameters for sizing
- Return a `FacetGrid` object, not an Axes
- Legend is placed outside the plot by default

### The Hierarchy

```
Figure-Level    Axes-Level Counterparts
──────────────────────────────────────
relplot()   →   scatterplot(), lineplot()
displot()   →   histplot(), kdeplot(), ecdfplot()
catplot()   →   barplot(), boxplot(), violinplot(),
                stripplot(), swarmplot(), countplot(),
                pointplot(), boxenplot()
```

### Side-by-Side Comparison

```python
# Axes-level: draws on existing/current axes
sns.histplot(data=tips, x="total_bill")
plt.show()

# Figure-level: creates its own figure and FacetGrid
sns.displot(data=tips, x="total_bill")
plt.show()

# Figure-level: adds faceting with a single argument
sns.displot(data=tips, x="total_bill", col="sex")
plt.show()
```

### Using ax= with Axes-Level Functions

```python
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

sns.histplot(data=tips, x="total_bill", ax=axes[0])
axes[0].set_title("Total Bill Distribution")

sns.histplot(data=tips, x="tip", ax=axes[1])
axes[1].set_title("Tip Distribution")

plt.tight_layout()
plt.show()
```

### Figure-Level Sizing

```python
# height = height of each subplot in inches
# aspect = width/height ratio
sns.displot(data=tips, x="total_bill", col="sex", height=4, aspect=1.2)
plt.show()
```

---

## 3. Figure-Level Functions

### 3.1 `relplot()`

**Definition:** The figure-level function for relational plots. It wraps `scatterplot()` and `lineplot()` and supports faceting.

**When to Use:**
- Visualizing relationships between two numerical variables across subgroups
- Comparing trends between multiple categories in separate panels

```python
# Default: scatter plot
sns.relplot(data=tips, x="total_bill", y="tip", hue="smoker")
plt.show()
```

```python
# Switch to line plot with kind parameter
sns.relplot(
    data=tips,
    x="size",
    y="tip",
    kind="line",
    hue="smoker",
    style="smoker",
    markers=True,
    col="time"  # facet by time (Lunch/Dinner)
)
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `data` | DataFrame | `tips` |
| `x`, `y` | Column names for axes | `"total_bill"`, `"tip"` |
| `hue` | Color encoding by variable | `"smoker"` |
| `size` | Size encoding by variable | `"size"` |
| `style` | Marker style by variable | `"day"` |
| `kind` | Plot type | `"scatter"` (default), `"line"` |
| `col` | Facet by columns | `"sex"` |
| `row` | Facet by rows | `"time"` |
| `col_wrap` | Wrap columns at N | `2` |
| `height` | Height per subplot | `4` |
| `aspect` | Aspect ratio | `1.2` |
| `palette` | Color palette | `"deep"`, `"Set2"` |

```python
# Advanced: row and column faceting
sns.relplot(
    data=tips,
    x="total_bill",
    y="tip",
    hue="day",
    col="sex",
    row="time",
    height=3,
    aspect=1
)
plt.show()
```

---

### 3.2 `displot()`

**Definition:** The figure-level function for distribution plots. Wraps `histplot()`, `kdeplot()`, and `ecdfplot()`.

**When to Use:**
- Exploring how a variable is distributed across different groups
- Comparing distributions across facets without manually creating subplots

```python
# Default: histogram
sns.displot(data=tips, x="total_bill", hue="sex", multiple="stack")
plt.show()
```

```python
# KDE plot
sns.displot(data=tips, x="total_bill", kind="kde", hue="sex", fill=True)
plt.show()
```

```python
# ECDF plot with faceting
sns.displot(data=tips, x="total_bill", kind="ecdf", col="day", height=3)
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `kind` | Plot type | `"hist"` (default), `"kde"`, `"ecdf"` |
| `hue` | Color grouping | `"sex"` |
| `multiple` | How to handle hue groups | `"layer"`, `"stack"`, `"dodge"`, `"fill"` |
| `fill` | Fill area under KDE | `True`, `False` |
| `bins` | Histogram bin count | `20`, `"auto"` |
| `col`, `row` | Faceting variables | `"sex"`, `"day"` |
| `rug` | Add rug plot | `True`, `False` |

---

### 3.3 `catplot()`

**Definition:** The figure-level function for categorical plots. Wraps all categorical axes-level functions.

**When to Use:**
- Comparing a numeric variable across categories with faceting
- Building complex multi-panel categorical summaries

```python
# Default: strip plot
sns.catplot(data=tips, x="day", y="total_bill")
plt.show()
```

```python
# Box plot with faceting
sns.catplot(
    data=tips,
    x="day",
    y="total_bill",
    kind="box",
    hue="sex",
    col="time",
    height=4
)
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `kind` | Plot type | `"strip"`, `"swarm"`, `"box"`, `"violin"`, `"bar"`, `"count"`, `"point"`, `"boxen"` |
| `hue` | Color grouping | `"smoker"` |
| `col`, `row` | Faceting | `"sex"`, `"time"` |
| `order` | Category order | `["Thur", "Fri", "Sat", "Sun"]` |
| `palette` | Color palette | `"pastel"`, `"muted"` |
| `height`, `aspect` | Figure sizing | `4`, `1.2` |

```python
# Violin with faceting
sns.catplot(
    data=tips,
    x="day",
    y="total_bill",
    kind="violin",
    hue="sex",
    split=True,      # split violins by hue
    palette="pastel",
    height=5
)
plt.show()
```

---

## 4. Relational Plots (Axes-Level)

### 4.1 `scatterplot()`

**Definition:** Displays the relationship between two numerical variables as individual data points on a 2D plane.

**When to Use:**
- Checking for correlation between two continuous variables
- Identifying clusters, outliers, or trends
- Comparing groups when each data point represents an observation

```python
# Basic scatter plot
sns.scatterplot(data=tips, x="total_bill", y="tip")
plt.show()
```

```python
# With hue, size, and style
sns.scatterplot(
    data=tips,
    x="total_bill",
    y="tip",
    hue="day",          # color by day
    size="size",        # point size by party size
    style="smoker",     # marker style by smoking status
    palette="deep",
    sizes=(20, 200)     # min and max point sizes
)
plt.title("Total Bill vs Tip")
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Axis variables | `"total_bill"`, `"tip"` |
| `hue` | Color encoding | `"day"` |
| `size` | Point size encoding | `"size"` |
| `style` | Marker style encoding | `"smoker"` |
| `palette` | Color palette | `"deep"`, `"viridis"` |
| `sizes` | (min, max) point sizes | `(20, 200)` |
| `alpha` | Transparency | `0.6` |
| `marker` | Marker shape | `"o"`, `"^"`, `"s"` |
| `ax` | Target axes | `axes[0]` |

```python
# Real-world: penguin bill dimensions by species
sns.scatterplot(
    data=penguins,
    x="bill_length_mm",
    y="bill_depth_mm",
    hue="species",
    style="island",
    alpha=0.8,
    palette="Set2"
)
plt.title("Penguin Bill Dimensions by Species")
plt.show()
```

---

### 4.2 `lineplot()`

**Definition:** Connects data points with lines to show trends over a continuous variable (often time). Automatically computes mean and confidence interval when multiple observations exist per x-value.

**When to Use:**
- Time series data
- Showing average trends across groups
- Comparing multiple group trajectories over time

```python
# Basic line plot
sns.lineplot(data=tips, x="size", y="tip")
plt.show()
```

```python
# With confidence interval by group
sns.lineplot(
    data=tips,
    x="size",
    y="total_bill",
    hue="sex",
    style="smoker",
    markers=True,
    dashes=False,
    errorbar="ci"       # show 95% confidence interval
)
plt.title("Total Bill vs Party Size")
plt.show()
```

```python
# Time-series style with flights dataset
flights_avg = flights.groupby("year")["passengers"].mean().reset_index()

sns.lineplot(
    data=flights_avg,
    x="year",
    y="passengers",
    marker="o",
    color="steelblue",
    linewidth=2.5
)
plt.title("Average Airline Passengers Over Time")
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Axis variables | `"year"`, `"passengers"` |
| `hue` | Color grouping | `"sex"` |
| `style` | Line style grouping | `"smoker"` |
| `markers` | Show markers | `True`, `False` |
| `dashes` | Use dashed lines | `True`, `False` |
| `errorbar` | Error bar type | `"ci"`, `"sd"`, `"se"`, `None` |
| `estimator` | Aggregation function | `"mean"`, `np.median` |
| `linewidth` | Line thickness | `2.5` |
| `alpha` | Transparency | `0.7` |

---

## 5. Distribution Plots (Axes-Level)

### 5.1 `histplot()`

**Definition:** Displays the distribution of a continuous or discrete variable by dividing data into bins and counting occurrences.

**When to Use:**
- Understanding the spread and shape of a variable
- Identifying skewness, multimodality, or outliers
- Comparing distributions between groups

```python
# Basic histogram
sns.histplot(data=tips, x="total_bill")
plt.show()
```

```python
# Overlapping histograms with KDE
sns.histplot(
    data=tips,
    x="total_bill",
    hue="sex",
    multiple="stack",   # options: "layer", "dodge", "stack", "fill"
    kde=True,           # overlay KDE curve
    bins=20,
    palette="Set1",
    alpha=0.6
)
plt.title("Total Bill Distribution by Sex")
plt.show()
```

```python
# 2D histogram (bivariate)
sns.histplot(data=penguins, x="flipper_length_mm", y="body_mass_g")
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Variable(s) | `"total_bill"` |
| `hue` | Color grouping | `"sex"` |
| `bins` | Number of bins | `20`, `"auto"`, `"fd"` |
| `binwidth` | Width of each bin | `5` |
| `kde` | Overlay KDE | `True`, `False` |
| `multiple` | Hue overlap style | `"layer"`, `"stack"`, `"dodge"`, `"fill"` |
| `stat` | Y-axis statistic | `"count"`, `"frequency"`, `"density"`, `"probability"` |
| `cumulative` | Cumulative histogram | `True`, `False` |
| `fill` | Fill bars | `True`, `False` |

---

### 5.2 `kdeplot()`

**Definition:** Visualizes the probability density function (PDF) of a continuous variable using kernel density estimation — a smoothed version of the histogram.

**When to Use:**
- Showing the shape of a distribution without the dependency on bin size
- Comparing smooth density estimates between groups
- Bivariate density visualization

```python
# Basic KDE plot
sns.kdeplot(data=tips, x="total_bill")
plt.show()
```

```python
# Filled KDE for multiple groups
sns.kdeplot(
    data=tips,
    x="total_bill",
    hue="day",
    fill=True,
    alpha=0.4,
    palette="tab10",
    common_norm=False    # each group normalized independently
)
plt.title("KDE: Total Bill by Day")
plt.show()
```

```python
# 2D density contour plot
sns.kdeplot(
    data=penguins,
    x="bill_length_mm",
    y="bill_depth_mm",
    hue="species",
    fill=True,
    alpha=0.3,
    thresh=0.05          # threshold for lowest contour
)
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Variable(s) | `"total_bill"` |
| `hue` | Color grouping | `"sex"` |
| `fill` | Fill under curve | `True`, `False` |
| `bw_adjust` | Bandwidth smoothing | `0.5` (narrow), `2` (wide) |
| `common_norm` | Normalize across groups | `True`, `False` |
| `cumulative` | Show cumulative KDE | `True`, `False` |
| `levels` | Number of contour levels (2D) | `10` |
| `thresh` | Minimum contour threshold | `0.05` |
| `alpha` | Transparency | `0.4` |

---

### 5.3 `ecdfplot()`

**Definition:** Plots the Empirical Cumulative Distribution Function (ECDF), showing the proportion of data points at or below each value.

**When to Use:**
- Comparing distributions without assumptions about shape
- Checking what percentage of data falls below a threshold
- A non-parametric alternative to the KDE plot

```python
# Basic ECDF
sns.ecdfplot(data=tips, x="total_bill")
plt.show()
```

```python
# Compare groups with ECDF
sns.ecdfplot(
    data=tips,
    x="total_bill",
    hue="day",
    palette="Set2",
    linewidth=2
)
plt.title("ECDF: Total Bill by Day")
plt.axvline(20, color="red", linestyle="--", label="$20 threshold")
plt.legend()
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x` | Variable | `"total_bill"` |
| `hue` | Color grouping | `"day"` |
| `stat` | Y-axis statistic | `"proportion"` (default), `"count"`, `"percent"` |
| `complementary` | Survival function (1-ECDF) | `True`, `False` |
| `linewidth` | Line thickness | `2` |

---

### 5.4 `rugplot()`

**Definition:** Draws small tick marks along an axis to show individual data point locations. Usually combined with other distribution plots.

**When to Use:**
- Adding raw data visibility to a KDE or histogram
- Checking density in specific value ranges
- Bivariate data density alongside scatter plots

```python
# Standalone rug plot
sns.rugplot(data=tips, x="total_bill")
plt.show()
```

```python
# Rug plot combined with KDE
fig, ax = plt.subplots(figsize=(8, 4))
sns.kdeplot(data=tips, x="total_bill", fill=True, ax=ax)
sns.rugplot(data=tips, x="total_bill", ax=ax, height=0.05, color="red")
plt.title("KDE with Rug Plot")
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Variable(s) | `"total_bill"` |
| `hue` | Color grouping | `"sex"` |
| `height` | Tick height (fraction of axis) | `0.05` |
| `expand_margins` | Expand axes margins | `True`, `False` |

---

## 6. Categorical Plots (Axes-Level)

### 6.1 `barplot()`

**Definition:** Shows the estimated central tendency (default: mean) of a numeric variable for each category as rectangular bars, with error bars showing uncertainty.

**When to Use:**
- Comparing average values across categories
- Showing group-level summaries with uncertainty
- Sales by region, average score by group, etc.

```python
# Basic bar plot
sns.barplot(data=tips, x="day", y="total_bill")
plt.show()
```

```python
# Grouped bar plot with customization
sns.barplot(
    data=tips,
    x="day",
    y="total_bill",
    hue="sex",
    palette="pastel",
    errorbar="sd",         # standard deviation instead of CI
    capsize=0.1,           # add caps to error bars
    order=["Thur", "Fri", "Sat", "Sun"]
)
plt.title("Average Total Bill by Day and Sex")
plt.ylabel("Average Total Bill ($)")
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Variables | `"day"`, `"total_bill"` |
| `hue` | Grouping | `"sex"` |
| `estimator` | Aggregation function | `"mean"` (default), `"median"`, `np.sum` |
| `errorbar` | Error bar style | `"ci"`, `"sd"`, `"se"`, `"pi"`, `None` |
| `capsize` | Error bar cap size | `0.1` |
| `order` | Category order | `["Thur", "Fri", "Sat", "Sun"]` |
| `orient` | Orientation | `"v"` (vertical), `"h"` (horizontal) |
| `width` | Bar width | `0.8` |
| `palette` | Color palette | `"pastel"` |

```python
# Horizontal bar plot
sns.barplot(
    data=tips,
    x="total_bill",
    y="day",
    orient="h",
    palette="rocket_r"
)
plt.title("Average Bill by Day (Horizontal)")
plt.show()
```

---

### 6.2 `countplot()`

**Definition:** A bar plot where the bar height represents the count of observations in each category.

**When to Use:**
- Showing the frequency of categories in a dataset
- Comparing how common each class/label is
- Class imbalance in machine learning datasets

```python
# Basic count plot
sns.countplot(data=tips, x="day")
plt.show()
```

```python
# Grouped count plot
sns.countplot(
    data=tips,
    x="day",
    hue="sex",
    palette="Set2",
    order=tips["day"].value_counts().index   # sort by most common
)
plt.title("Number of Visits by Day and Sex")
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x` or `y` | Category variable | `"day"`, `"sex"` |
| `hue` | Grouping | `"smoker"` |
| `order` | Bar order | `["Sat", "Sun", "Thur", "Fri"]` |
| `palette` | Color palette | `"Set2"` |
| `stat` | Y-axis statistic | `"count"` (default), `"percent"`, `"proportion"` |
| `orient` | Orientation | `"v"`, `"h"` |

---

### 6.3 `boxplot()`

**Definition:** Shows the five-number summary (minimum, Q1, median, Q3, maximum) and outliers for a numeric variable grouped by categories.

**When to Use:**
- Comparing distributions between groups compactly
- Detecting outliers in data
- Examining spread and skewness at a glance

```python
# Basic box plot
sns.boxplot(data=tips, x="day", y="total_bill")
plt.show()
```

```python
# Grouped box plot with customization
sns.boxplot(
    data=tips,
    x="day",
    y="total_bill",
    hue="smoker",
    palette="Set3",
    notch=True,             # notch shows CI around median
    flierprops=dict(marker="x", color="red", markersize=8),  # outlier style
    order=["Thur", "Fri", "Sat", "Sun"]
)
plt.title("Total Bill Distribution by Day")
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Variables | `"day"`, `"total_bill"` |
| `hue` | Grouping | `"smoker"` |
| `notch` | Notch for median CI | `True`, `False` |
| `whis` | Whisker length (IQR multiplier) | `1.5` (default), `2.5` |
| `flierprops` | Outlier point style | `dict(marker="o", color="red")` |
| `width` | Box width | `0.8` |
| `linewidth` | Box edge thickness | `1.5` |
| `palette` | Color palette | `"Set3"` |
| `saturation` | Color saturation | `0.75` |

---

### 6.4 `violinplot()`

**Definition:** Combines a box plot with a kernel density estimate to show the full distribution shape, including multimodality.

**When to Use:**
- When you want to see the full distribution shape, not just summary stats
- Comparing multi-modal distributions between groups
- More informative than a box plot for large datasets

```python
# Basic violin plot
sns.violinplot(data=tips, x="day", y="total_bill")
plt.show()
```

```python
# Split violin with hue
sns.violinplot(
    data=tips,
    x="day",
    y="total_bill",
    hue="sex",
    split=True,            # mirror the two groups within one violin
    palette="muted",
    inner="quartile",      # show quartile lines inside violin
    cut=0                  # don't extend beyond observed data
)
plt.title("Bill Distribution by Day (Split by Sex)")
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Variables | `"day"`, `"total_bill"` |
| `hue` | Grouping | `"sex"` |
| `split` | Mirror two hue groups | `True`, `False` |
| `inner` | Interior marks | `"box"`, `"quart"`, `"point"`, `"stick"`, `None` |
| `cut` | Range beyond data | `0` (clip), `2` (extend) |
| `bw_adjust` | Bandwidth smoothing | `0.5`, `1`, `2` |
| `scale` | Violin scaling method | `"area"`, `"count"`, `"width"` |
| `linewidth` | Outline thickness | `1.5` |
| `palette` | Color palette | `"muted"` |

---

### 6.5 `stripplot()`

**Definition:** Shows all individual data points for one or more categories, jittered horizontally to reduce overlap.

**When to Use:**
- Small to medium datasets where individual points matter
- Overlaid on box or violin plots to show raw data
- Auditing exactly where data points fall

```python
# Basic strip plot
sns.stripplot(data=tips, x="day", y="total_bill")
plt.show()
```

```python
# Strip over box plot
fig, ax = plt.subplots(figsize=(8, 5))
sns.boxplot(data=tips, x="day", y="total_bill", palette="pastel", ax=ax, width=0.5)
sns.stripplot(
    data=tips,
    x="day",
    y="total_bill",
    hue="sex",
    ax=ax,
    dodge=True,       # separate points by hue
    alpha=0.7,
    jitter=0.2,       # amount of horizontal jitter
    size=5
)
plt.title("Bill Distribution with Raw Data Points")
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Variables | `"day"`, `"total_bill"` |
| `hue` | Color grouping | `"sex"` |
| `jitter` | Horizontal jitter amount | `True`, `0.2` |
| `dodge` | Separate by hue | `True`, `False` |
| `size` | Point size | `5` |
| `alpha` | Transparency | `0.7` |
| `marker` | Marker shape | `"o"`, `"D"` |

---

### 6.6 `swarmplot()`

**Definition:** Similar to a strip plot but positions points to avoid overlap, giving a clearer view of the distribution density.

**When to Use:**
- Small to medium datasets where overlap in a strip plot would be misleading
- Showing all individual data points without overlaps
- Combined with violin or box plots for complete distribution views

```python
# Basic swarm plot
sns.swarmplot(data=tips, x="day", y="total_bill")
plt.show()
```

```python
# Swarm with hue and size
sns.swarmplot(
    data=tips,
    x="day",
    y="total_bill",
    hue="smoker",
    dodge=True,
    palette="colorblind",
    size=4,
    order=["Thur", "Fri", "Sat", "Sun"]
)
plt.title("All Tips by Day (Non-Overlapping)")
plt.show()
```

> ⚠️ **Note:** Swarm plots are slow for large datasets (>1000 points). Use strip plots instead.

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Variables | `"day"`, `"total_bill"` |
| `hue` | Color grouping | `"smoker"` |
| `dodge` | Separate by hue | `True`, `False` |
| `size` | Point size | `4` |
| `palette` | Colors | `"colorblind"` |
| `order` | Category order | `["Thur", "Fri", "Sat", "Sun"]` |

---

### 6.7 `pointplot()`

**Definition:** Shows the estimated central tendency and confidence interval for a numeric variable across categories, connected by lines to highlight trends.

**When to Use:**
- Comparing means across ordered categories
- Showing interaction effects between two categorical variables
- When you care about trends in means, not distributions

```python
# Basic point plot
sns.pointplot(data=tips, x="day", y="total_bill")
plt.show()
```

```python
# Interaction plot
sns.pointplot(
    data=tips,
    x="day",
    y="total_bill",
    hue="sex",
    palette={"Male": "steelblue", "Female": "salmon"},
    markers=["o", "D"],
    linestyles=["-", "--"],
    dodge=0.3,             # separate lines horizontally
    errorbar="ci",
    capsize=0.1
)
plt.title("Mean Bill by Day (Interaction by Sex)")
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Variables | `"day"`, `"total_bill"` |
| `hue` | Grouping | `"sex"` |
| `estimator` | Aggregation | `"mean"`, `np.median` |
| `errorbar` | Error bars | `"ci"`, `"sd"`, `None` |
| `markers` | Marker per hue | `["o", "D"]` |
| `linestyles` | Line styles per hue | `["-", "--"]` |
| `dodge` | Separation amount | `0.3` |
| `join` | Connect points | `True`, `False` |

---

### 6.8 `boxenplot()`

**Definition:** An enhanced box plot ("letter-value plot") that shows more quantiles for large datasets, providing a better view of the distribution tails.

**When to Use:**
- Large datasets (>1000 observations) where a regular box plot is insufficient
- When you want to show more percentiles than Q1/Q3
- Investigating the distribution of extreme values

```python
# Basic boxen plot
sns.boxenplot(data=tips, x="day", y="total_bill")
plt.show()
```

```python
# Customized boxen plot
sns.boxenplot(
    data=tips,
    x="day",
    y="total_bill",
    hue="smoker",
    palette="husl",
    k_depth="full",         # number of quantile levels
    outlier_prop=0.01,      # proportion treated as outliers
    width=0.7
)
plt.title("Letter-Value Plot: Total Bill by Day")
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Variables | `"day"`, `"total_bill"` |
| `hue` | Grouping | `"smoker"` |
| `k_depth` | Quantile depth method | `"tukey"`, `"proportion"`, `"trustworthy"`, `"full"` |
| `outlier_prop` | Outlier threshold | `0.01` |
| `width` | Box width | `0.7` |
| `palette` | Colors | `"husl"` |

---

## 7. Matrix / Heatmap Plots

### 7.1 `heatmap()`

**Definition:** Represents a matrix of values as colors in a 2D grid, making it easy to spot patterns and correlations.

**When to Use:**
- Visualizing correlation matrices
- Showing tabular data like monthly sales or passenger counts
- Feature importance matrices in ML
- Confusion matrices for model evaluation

```python
# Correlation heatmap
corr = tips.select_dtypes(include="number").corr()

sns.heatmap(corr, annot=True, fmt=".2f", cmap="coolwarm", center=0)
plt.title("Correlation Matrix")
plt.show()
```

```python
# Flights dataset heatmap
flights_pivot = flights.pivot(index="month", columns="year", values="passengers")

sns.heatmap(
    flights_pivot,
    annot=True,
    fmt="d",
    cmap="YlOrRd",
    linewidths=0.5,
    linecolor="white",
    cbar_kws={"label": "Passengers"}
)
plt.title("Monthly Airline Passengers (1949–1960)")
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `data` | 2D array or DataFrame | `corr_matrix` |
| `annot` | Show values in cells | `True`, `False` |
| `fmt` | Format of annotations | `".2f"`, `"d"`, `".0%"` |
| `cmap` | Color map | `"coolwarm"`, `"viridis"`, `"YlOrRd"` |
| `center` | Center the colormap | `0` |
| `vmin`, `vmax` | Color range bounds | `-1`, `1` |
| `linewidths` | Grid line width | `0.5` |
| `linecolor` | Grid line color | `"white"` |
| `mask` | Boolean mask for cells | `np.triu(np.ones(...))` |
| `square` | Force square cells | `True` |
| `cbar_kws` | Colorbar options | `{"label": "Value"}` |

```python
# Mask upper triangle (for symmetric correlation matrices)
import numpy as np

mask = np.triu(np.ones_like(corr, dtype=bool))
sns.heatmap(corr, mask=mask, annot=True, fmt=".2f", cmap="coolwarm",
            square=True, linewidths=0.5)
plt.title("Lower Triangle Correlation Heatmap")
plt.show()
```

---

### 7.2 `clustermap()`

**Definition:** A heatmap where rows and/or columns are hierarchically clustered and reordered to group similar patterns together.

**When to Use:**
- Gene expression data analysis (bioinformatics)
- Grouping similar features or samples automatically
- Finding patterns in complex matrices

```python
# Basic cluster map
sns.clustermap(flights_pivot, cmap="viridis", figsize=(10, 8))
plt.show()
```

```python
# Normalized cluster map
sns.clustermap(
    flights_pivot,
    cmap="coolwarm",
    standard_scale=1,       # normalize each column
    col_cluster=True,
    row_cluster=True,
    linewidths=0.3,
    figsize=(12, 10),
    dendrogram_ratio=0.1    # reduce dendrogram size
)
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `data` | 2D DataFrame | `flights_pivot` |
| `method` | Clustering method | `"single"`, `"complete"`, `"average"`, `"ward"` |
| `metric` | Distance metric | `"euclidean"`, `"correlation"` |
| `standard_scale` | Normalize by row/col | `0` (row), `1` (col) |
| `z_score` | Z-score normalization | `0` (row), `1` (col) |
| `row_cluster` | Cluster rows | `True`, `False` |
| `col_cluster` | Cluster columns | `True`, `False` |
| `cmap` | Color map | `"viridis"` |
| `figsize` | Figure size | `(10, 8)` |

---

## 8. Regression Plots

### 8.1 `lmplot()`

**Definition:** Figure-level function that plots scatter data with a linear regression fit and confidence interval. Supports faceting.

**When to Use:**
- Exploring linear relationships between variables
- Comparing regression fits across groups/categories
- Quick regression visualization with faceting

```python
# Basic regression plot
sns.lmplot(data=tips, x="total_bill", y="tip")
plt.show()
```

```python
# Faceted regression by sex and time
sns.lmplot(
    data=tips,
    x="total_bill",
    y="tip",
    hue="smoker",
    col="sex",
    row="time",
    height=3,
    aspect=1.1,
    scatter_kws={"alpha": 0.5},
    line_kws={"linewidth": 2}
)
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Variables | `"total_bill"`, `"tip"` |
| `hue` | Color grouping | `"smoker"` |
| `col`, `row` | Faceting | `"sex"`, `"time"` |
| `order` | Polynomial order | `1` (linear), `2` (quadratic) |
| `ci` | Confidence interval | `95` (default), `None` |
| `scatter` | Show scatter | `True`, `False` |
| `fit_reg` | Show regression | `True`, `False` |
| `robust` | Robust regression | `True`, `False` |
| `logx` | Log-scale x | `True`, `False` |
| `scatter_kws` | Scatter point kwargs | `{"alpha": 0.5}` |
| `line_kws` | Line kwargs | `{"linewidth": 2}` |

---

### 8.2 `regplot()`

**Definition:** Axes-level version of `lmplot()`. Plots a scatter diagram with a regression line and CI band.

**When to Use:**
- Same as lmplot() but when composing into custom matplotlib figures
- When you need precise axes control

```python
# Basic regplot
sns.regplot(data=tips, x="total_bill", y="tip")
plt.show()
```

```python
# Polynomial regression (quadratic)
sns.regplot(
    data=tips,
    x="total_bill",
    y="tip",
    order=2,                        # 2nd-degree polynomial
    ci=90,                          # 90% confidence interval
    scatter_kws={"color": "gray", "alpha": 0.5},
    line_kws={"color": "red", "linewidth": 2}
)
plt.title("Tip vs Total Bill (Polynomial Fit)")
plt.show()
```

```python
# Combine regplot with other plots
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

sns.regplot(data=tips[tips["sex"] == "Male"],
            x="total_bill", y="tip", ax=axes[0], label="Male")
sns.regplot(data=tips[tips["sex"] == "Female"],
            x="total_bill", y="tip", ax=axes[1], label="Female", color="salmon")

axes[0].set_title("Male")
axes[1].set_title("Female")
plt.tight_layout()
plt.show()
```

---

### 8.3 `residplot()`

**Definition:** Plots residuals (observed minus predicted) from a regression, helping diagnose whether linear regression assumptions hold.

**When to Use:**
- Diagnosing regression model fit
- Checking for non-linearity, heteroscedasticity, or patterns in errors

```python
sns.residplot(
    data=tips,
    x="total_bill",
    y="tip",
    lowess=True,    # add LOWESS smoother to highlight trends
    color="steelblue",
    scatter_kws={"alpha": 0.5}
)
plt.axhline(0, color="red", linestyle="--")
plt.title("Regression Residuals")
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `x`, `y` | Variables | `"total_bill"`, `"tip"` |
| `lowess` | Add LOWESS trend | `True`, `False` |
| `order` | Polynomial order of fit | `1`, `2` |
| `scatter_kws` | Scatter style kwargs | `{"alpha": 0.5}` |

---

## 9. Multi-Plot Grids

### 9.1 `pairplot()`

**Definition:** Creates a grid of scatter plots for every pair of numeric variables in a dataset, with histograms or KDE plots on the diagonal.

**When to Use:**
- Exploratory data analysis on a new dataset
- Detecting correlations and patterns across multiple variables
- Quick multivariate overview with group coloring

```python
# Basic pair plot
sns.pairplot(tips)
plt.show()
```

```python
# With hue and customizations
sns.pairplot(
    tips,
    hue="smoker",
    palette="husl",
    diag_kind="kde",         # KDE on diagonal instead of histogram
    plot_kws={"alpha": 0.5},
    diag_kws={"fill": True},
    corner=True              # show only lower triangle
)
plt.show()
```

```python
# Select specific variables
sns.pairplot(
    penguins.dropna(),
    vars=["bill_length_mm", "bill_depth_mm", "flipper_length_mm", "body_mass_g"],
    hue="species",
    palette="Set2"
)
plt.show()
```

**Key Arguments:**

| Argument | Description | Example Values |
|---|---|---|
| `data` | DataFrame | `tips` |
| `hue` | Color grouping | `"species"` |
| `vars` | Select variables | `["col1", "col2"]` |
| `diag_kind` | Diagonal plot type | `"auto"`, `"hist"`, `"kde"`, `None` |
| `kind` | Off-diagonal plot type | `"scatter"`, `"kde"`, `"hist"`, `"reg"` |
| `plot_kws` | Off-diagonal kwargs | `{"alpha": 0.5}` |
| `diag_kws` | Diagonal plot kwargs | `{"bins": 20}` |
| `corner` | Show only lower triangle | `True`, `False` |
| `palette` | Color palette | `"Set2"` |

---

### 9.2 `FacetGrid`

**Definition:** A low-level class for building multi-subplot grids where each subplot shows a subset of the data based on a variable's value.

**When to Use:**
- When figure-level functions don't offer enough flexibility
- Building custom multi-panel figures
- Applying any plotting function across data subsets

```python
# FacetGrid: histograms per day
g = sns.FacetGrid(tips, col="day", height=3, aspect=1)
g.map(sns.histplot, "total_bill", bins=15)
g.set_axis_labels("Total Bill ($)", "Count")
g.set_titles("{col_name}")
g.add_legend()
plt.show()
```

```python
# 2D FacetGrid: scatter plots by sex and time
g = sns.FacetGrid(tips, col="sex", row="time", height=3, aspect=1)
g.map_dataframe(sns.scatterplot, x="total_bill", y="tip", alpha=0.7)
g.set_axis_labels("Total Bill", "Tip")
plt.show()
```

**Key FacetGrid methods:**

| Method | Description |
|---|---|
| `.map(func, *args)` | Apply a function to each subplot |
| `.map_dataframe(func, **kwargs)` | Apply a DataFrame-aware function |
| `.set_axis_labels(x, y)` | Set axis labels for all subplots |
| `.set_titles(template)` | Set subplot titles (use `{col_name}`) |
| `.add_legend()` | Add a shared legend |
| `.set(xlim=, ylim=)` | Set shared axis limits |

---

### 9.3 `PairGrid`

**Definition:** Low-level class for creating pair plots with different plot types for the upper triangle, lower triangle, and diagonal.

**When to Use:**
- When you need asymmetric pair plots (e.g., scatter below, KDE above)
- Full control over what is plotted in each section of the grid

```python
g = sns.PairGrid(penguins.dropna(), hue="species", palette="Set2")

g.map_upper(sns.scatterplot, alpha=0.5)          # upper triangle: scatter
g.map_lower(sns.kdeplot, fill=True, alpha=0.3)   # lower triangle: KDE
g.map_diag(sns.histplot, bins=15)                # diagonal: histogram

g.add_legend()
plt.show()
```

**Key PairGrid Methods:**

| Method | Description |
|---|---|
| `.map_upper(func)` | Plot in upper triangle |
| `.map_lower(func)` | Plot in lower triangle |
| `.map_diag(func)` | Plot on diagonal |
| `.map(func)` | Plot everywhere |
| `.add_legend()` | Add shared legend |

---

## 10. Themes and Aesthetics

Seaborn provides built-in themes that control the overall look of all plots.

### Setting a Theme

```python
sns.set_theme(style="darkgrid")   # applies globally
```

### Available Styles

| Style | Description |
|---|---|
| `"darkgrid"` | Dark background with grid lines (default) |
| `"whitegrid"` | White background with grid lines |
| `"dark"` | Dark background, no grid |
| `"white"` | White background, no grid |
| `"ticks"` | White background with tick marks |

```python
styles = ["darkgrid", "whitegrid", "dark", "white", "ticks"]

fig, axes = plt.subplots(1, len(styles), figsize=(20, 3))
for i, style in enumerate(styles):
    with sns.axes_style(style):     # temporary style in context manager
        sns.histplot(data=tips, x="total_bill", ax=axes[i])
        axes[i].set_title(style)
plt.tight_layout()
plt.show()
```

### Context Presets

Context scales font sizes and line widths for different output sizes.

```python
sns.set_context("paper")    # smallest
sns.set_context("notebook") # default
sns.set_context("talk")     # larger fonts for presentations
sns.set_context("poster")   # largest
```

### Custom rc Parameters

```python
sns.set_theme(
    style="whitegrid",
    context="talk",
    font="Arial",
    font_scale=1.2,
    rc={
        "axes.spines.right": False,
        "axes.spines.top": False,
        "figure.figsize": (10, 6)
    }
)
```

---

## 11. Color Palettes

### Qualitative (Categorical) Palettes

```python
# Best for unordered categories
palettes = ["deep", "muted", "pastel", "bright", "dark", "colorblind", "Set1", "Set2", "tab10"]

for p in palettes:
    sns.palplot(sns.color_palette(p))
    plt.title(p)
    plt.show()
```

### Sequential Palettes

```python
# Best for ordered/continuous data
seq_palettes = ["Blues", "Greens", "viridis", "plasma", "rocket", "mako", "flare"]
```

### Diverging Palettes

```python
# Best for data with a meaningful center (e.g., correlations)
div_palettes = ["coolwarm", "RdBu", "vlag", "icefire"]
```

### Applying a Palette

```python
# In any plot
sns.barplot(data=tips, x="day", y="total_bill", palette="Set2")

# Set globally
sns.set_palette("colorblind")

# Custom palette
custom = ["#e74c3c", "#3498db", "#2ecc71", "#f39c12"]
sns.barplot(data=tips, x="day", y="total_bill", palette=custom)
```

### Continuous Hue Mapping

```python
sns.scatterplot(
    data=penguins,
    x="flipper_length_mm",
    y="body_mass_g",
    hue="bill_length_mm",   # continuous variable
    palette="viridis",
    size="bill_length_mm",
    sizes=(20, 200)
)
plt.show()
```

---

## 12. Quick Reference Cheat Sheet

### Plot Type Selector

| Goal | Best Plot |
|---|---|
| Two continuous variables | `scatterplot()` |
| Trend over ordered x values | `lineplot()` |
| Distribution of one variable | `histplot()`, `kdeplot()` |
| Distribution with cumulative % | `ecdfplot()` |
| Show raw points per category | `stripplot()`, `swarmplot()` |
| Compare category means | `barplot()`, `pointplot()` |
| Compare category distributions | `boxplot()`, `violinplot()`, `boxenplot()` |
| Count of each category | `countplot()` |
| Matrix patterns / correlations | `heatmap()` |
| Clustered patterns | `clustermap()` |
| Regression + scatter | `regplot()`, `lmplot()` |
| All pairwise relationships | `pairplot()` |
| Custom multi-panel grid | `FacetGrid`, `PairGrid` |

### Figure-Level Quick Selector

| Module | Figure-Level | Kinds Available |
|---|---|---|
| Relational | `relplot()` | `scatter`, `line` |
| Distribution | `displot()` | `hist`, `kde`, `ecdf` |
| Categorical | `catplot()` | `strip`, `swarm`, `box`, `violin`, `bar`, `count`, `point`, `boxen` |

### Top Customization Arguments (Universal)

| Argument | Effect |
|---|---|
| `hue` | Color-code by a variable |
| `palette` | Choose a color palette |
| `alpha` | Set transparency (0–1) |
| `ax` | Target a specific Axes (axes-level only) |
| `col` / `row` | Facet the figure (figure-level only) |
| `height` / `aspect` | Control figure size (figure-level only) |
| `order` | Set category display order |
| `estimator` | Aggregation function for bar/point plots |
| `errorbar` | Error bar style (`"ci"`, `"sd"`, `"se"`, `None`) |

---

*This course was compiled from [Seaborn Official Documentation](https://seaborn.pydata.org/), [GeeksForGeeks](https://www.geeksforgeeks.org/python/types-of-seaborn-plots/), and [Kaggle Seaborn Guide](https://www.kaggle.com/code/vijayjoshi17/seaborn-guide-all-important-plots).*
