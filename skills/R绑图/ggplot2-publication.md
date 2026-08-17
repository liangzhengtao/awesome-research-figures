# Publication-Quality ggplot2 Figures

## When to Use

- Creating figures for academic papers using R
- Generating multi-panel figures with faceting
- Producing statistical visualizations with built-in stat layers
- Need fine-grained control over every visual element
- Working in fields where R is the standard (biostatistics, ecology, social sciences)

## Tools and Libraries

```r
install.packages(c("ggplot2", "ggpubr", "patchwork", "ggsci",
                    "scales", "cowplot", "ggridges", "ggrepel"))
```

## Step-by-Step Instructions

### 1. Set Up the Publication Theme

```r
library(ggplot2)
library(patchwork)

# Publication theme function
theme_publication <- function(base_size = 10, base_family = "serif") {
  theme_minimal(base_size = base_size, base_family = base_family) %+replace%
    theme(
      # Text
      plot.title = element_text(size = rel(1.2), hjust = 0.5,
                                face = "bold", margin = margin(b = 10)),
      axis.title = element_text(size = rel(1.0)),
      axis.text = element_text(size = rel(0.9), color = "black"),

      # Axes
      axis.line = element_line(color = "black", linewidth = 0.5),
      axis.ticks = element_line(color = "black", linewidth = 0.4),
      axis.ticks.length = unit(2, "pt"),

      # Panel
      panel.grid.major = element_line(color = "#E8E8E8", linewidth = 0.3),
      panel.grid.minor = element_blank(),
      panel.border = element_blank(),

      # Legend
      legend.title = element_text(size = rel(0.9)),
      legend.text = element_text(size = rel(0.85)),
      legend.key.size = unit(0.8, "lines"),
      legend.background = element_rect(fill = "white", color = NA),
      legend.key = element_rect(fill = "white", color = NA),

      # Strip (facet labels)
      strip.text = element_text(size = rel(0.9), face = "bold",
                                margin = margin(4, 4, 4, 4)),
      strip.background = element_rect(fill = "#F5F5F5", color = NA),

      # Plot margins
      plot.margin = margin(5, 10, 5, 5)
    )
}

# Color palettes
COLORS_PUBLICATION <- c("#0072B2", "#D55E00", "#009E73",
                         "#CC79A7", "#E69F00", "#56B4E9")

# Journal-specific themes
theme_nature <- function() {
  theme_publication(base_family = "sans") +
    theme(text = element_text(family = "Helvetica"))
}

theme_ieee <- function() {
  theme_publication(base_family = "serif") +
    theme(text = element_text(family = "Times New Roman"))
}
```

### 2. Journal Figure Sizes

```r
# Width in inches
FIG_SIZES <- list(
  nature_single  = c(3.504, 2.628),   # 89 mm
  nature_double  = c(7.205, 5.404),   # 183 mm
  ieee_single    = c(3.5, 2.8),       # 89 mm
  ieee_double    = c(7.16, 5.0),      # 182 mm
  science_single = c(3.42, 2.565),    # 87 mm
  science_double = c(7.0, 5.25)       # 178 mm
)
```

## Code Templates

### Template 1: Multi-Panel Figure with patchwork

```r
library(ggplot2)
library(patchwork)

create_multipanel <- function(df, filename = "multipanel.pdf") {
  # Panel A: Scatter plot
  p1 <- ggplot(df, aes(x = x_var, y = y_var, color = group)) +
    geom_point(size = 1.5, alpha = 0.7) +
    geom_smooth(method = "lm", se = TRUE, linewidth = 0.8) +
    scale_color_manual(values = COLORS_PUBLICATION) +
    labs(x = "X Variable", y = "Y Variable", tag = "A") +
    theme_publication() +
    theme(legend.position = "bottom")

  # Panel B: Box plot
  p2 <- ggplot(df, aes(x = group, y = value, fill = group)) +
    geom_boxplot(outlier.shape = NA, alpha = 0.7, width = 0.6) +
    geom_jitter(width = 0.15, size = 1, alpha = 0.5) +
    scale_fill_manual(values = COLORS_PUBLICATION) +
    labs(x = "", y = "Value", tag = "B") +
    theme_publication() +
    theme(legend.position = "none")

  # Panel C: Density plot
  p3 <- ggplot(df, aes(x = value, fill = group)) +
    geom_density(alpha = 0.4, linewidth = 0.6) +
    scale_fill_manual(values = COLORS_PUBLICATION) +
    labs(x = "Value", y = "Density", tag = "C") +
    theme_publication() +
    theme(legend.position = "bottom")

  # Panel D: Bar chart with error bars
  summary_df <- aggregate(value ~ group, data = df,
                          FUN = function(x) c(mean = mean(x), sd = sd(x)))
  summary_df <- do.call(data.frame, summary_df)

  p4 <- ggplot(summary_df, aes(x = group, y = value.mean, fill = group)) +
    geom_col(alpha = 0.7, width = 0.6, color = "black", linewidth = 0.3) +
    geom_errorbar(aes(ymin = value.mean - value.sd,
                       ymax = value.mean + value.sd),
                  width = 0.15, linewidth = 0.5) +
    scale_fill_manual(values = COLORS_PUBLICATION) +
    labs(x = "", y = "Mean ± SD", tag = "D") +
    theme_publication() +
    theme(legend.position = "none")

  # Compose layout
  layout <- "
  AABB
  CCDD
  "
  combined <- p1 + p2 + p3 + p4 +
    plot_layout(design = layout, guides = "collect") &
    theme(legend.position = "bottom")

  ggsave(filename, combined, width = 7, height = 6,
         dpi = 600, device = cairo_pdf)
  cat("Saved:", filename, "\n")
}

# Usage
set.seed(42)
df <- data.frame(
  x_var = rnorm(200),
  y_var = rnorm(200) + 0.5 * rnorm(200),
  group = sample(c("Control", "Treatment A", "Treatment B"), 200, replace = TRUE),
  value = rnorm(200, mean = rep(c(0, 1, 2), length.out = 200))
)
create_multipanel(df)
```

### Template 2: Survival Plot (Kaplan-Meier)

```r
library(survival)
library(survminer)

create_survival_plot <- function(surv_data, time_col, event_col, group_col,
                                  filename = "survival.pdf") {
  # Fit survival curves
  formula <- as.formula(paste0("Surv(", time_col, ", ", event_col, ") ~ ", group_col))
  fit <- survfit(formula, data = surv_data)

  # Plot with survminer
  ggsurv <- ggsurvplot(
    fit, data = surv_data,
    pval = TRUE,
    pval.method = TRUE,
    conf.int = TRUE,
    conf.int.alpha = 0.15,
    risk.table = TRUE,
    risk.table.col = "strata",
    risk.table.height = 0.25,
    linetype = "strata",
    palette = COLORS_PUBLICATION[1:length(fit$strata)],
    xlab = "Time (months)",
    ylab = "Survival Probability",
    legend.title = "",
    legend.labs = names(fit$strata),
    font.main = c(12, "bold", "serif"),
    font.x = c(10, "serif"),
    font.y = c(10, "serif"),
    font.tickslab = c(9, "serif"),
    ggtheme = theme_publication()
  )

  pdf(filename, width = 5, height = 5)
  print(ggsurv)
  dev.off()
  cat("Saved:", filename, "\n")
}
```

### Template 3: Forest Plot (Meta-Analysis)

```r
create_forest_plot <- function(data, filename = "forest.pdf") {
  # data: data.frame with columns study, effect, lower, upper, weight

  p <- ggplot(data, aes(x = effect, y = reorder(study, effect))) +
    # Confidence interval
    geom_errorbarh(aes(xmin = lower, xmax = upper),
                   height = 0.2, linewidth = 0.6, color = "#444444") +
    # Point estimate (size proportional to weight)
    geom_point(aes(size = weight), shape = 18, color = "#D55E00") +
    # Reference line
    geom_vline(xintercept = 0, linetype = "dashed", linewidth = 0.5,
               color = "#888888") +
    # Sizing
    scale_size_continuous(range = c(2, 6), guide = "none") +
    # Labels
    labs(x = "Effect Size (95% CI)", y = "", title = "") +
    theme_publication() +
    theme(
      panel.grid.major.y = element_blank(),
      axis.text.y = element_text(size = 9)
    )

  ggsave(filename, p, width = 6, height = max(3, nrow(data) * 0.4),
         dpi = 600, device = cairo_pdf)
  cat("Saved:", filename, "\n")
}

# Usage
data <- data.frame(
  study = paste("Study", LETTERS[1:8]),
  effect = c(-0.3, 0.1, 0.5, -0.1, 0.3, 0.7, 0.2, 0.4),
  lower = c(-0.6, -0.2, 0.2, -0.4, 0.0, 0.3, -0.1, 0.1),
  upper = c(0.0, 0.4, 0.8, 0.2, 0.6, 1.1, 0.5, 0.7),
  weight = c(10, 15, 8, 12, 20, 5, 18, 14)
)
create_forest_plot(data)
```

### Template 4: Ridge Plot (Joy Plot)

```r
library(ggridges)

create_ridge_plot <- function(df, x_var, y_var, filename = "ridge.pdf") {
  p <- ggplot(df, aes(x = .data[[x_var]], y = .data[[y_var]],
                       fill = .data[[y_var]])) +
    geom_density_ridges(scale = 1.5, alpha = 0.7,
                        linewidth = 0.4, color = "white") +
    scale_fill_manual(values = COLORS_PUBLICATION) +
    labs(x = x_var, y = "") +
    theme_publication() +
    theme(legend.position = "none")

  ggsave(filename, p, width = 5, height = max(3, nrow(unique(df[y_var])) * 0.5),
         dpi = 600, device = cairo_pdf)
}
```

## Style Specifications

| Parameter | Recommended |
|-----------|-------------|
| Base font size | 10 pt |
| Font family | serif (IEEE) or sans (Nature) |
| Line width (data) | 0.6–1.0 mm |
| Point size | 1.5–3 |
| Alpha (overlapping) | 0.5–0.7 |
| Grid lines | Major only, light gray |
| Export | `ggsave(..., device = cairo_pdf)` |

## Common Pitfalls

1. **Font embedding in PDF**: Use `cairo_pdf` device for proper font embedding
2. **Facet label wrapping**: Use `labeller = label_wrap_gen(width = 15)` for long labels
3. **Legend overlapping data**: Place outside with `theme(legend.position = "bottom")`
4. **Patchwork alignment**: Use `plot_layout(axes = "collect")` to align y-axes
5. **Color in grayscale**: Test with `scale_fill_grey()` or `scale_color_grey()`
6. **Missing `+` in ggplot chain**: Each layer must be added with `+`
7. **Factor ordering**: Use `fct_reorder()` for meaningful order instead of alphabetical

## Journal-Specific Tips

- **Nature**: Use `theme_nature()`; max 183 mm wide; Helvetica/Arial
- **IEEE**: Use `theme_ieee()`; Times New Roman; vector format (PDF/EPS)
- **PLOS**: 300 DPI minimum; TIFF or EPS; describe in figure legend
- **Cell**: Sans-serif fonts; support multi-page supplementary figures
- **General**: Always set `seed` for reproducible jitter; save source data as CSV
