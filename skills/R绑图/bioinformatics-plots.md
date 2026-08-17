# Bioinformatics Visualization

## When to Use

- Visualizing genomics/proteomics data: volcano plots, gene expression heatmaps
- Creating pathway diagrams, Sankey/alluvial diagrams
- Plotting gene ontology enrichment results
- Visualizing differential expression analysis output
- Creating figures for bioinformatics or systems biology papers

## Tools and Libraries

```r
# Bioconductor packages
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install(c("EnhancedVolcano", "ComplexHeatmap", "clusterProfiler"))

# CRAN packages
install.packages(c("ggplot2", "pheatmap", "ggalluvial", "ggrepel",
                    "RColorBrewer", "viridis"))
```

## Step-by-Step Instructions

### 1. Configure Bioinformatics Visualization Defaults

```r
library(ggplot2)

# Publication theme for bioinformatics figures
theme_bio <- function(base_size = 10) {
  theme_minimal(base_size = base_size) +
    theme(
      text = element_text(family = "sans", color = "black"),
      axis.title = element_text(size = rel(1.0)),
      axis.text = element_text(size = rel(0.85), color = "black"),
      axis.line = element_line(color = "black", linewidth = 0.4),
      axis.ticks = element_line(color = "black", linewidth = 0.3),
      panel.grid.major = element_line(color = "#F0F0F0", linewidth = 0.3),
      panel.grid.minor = element_blank(),
      legend.text = element_text(size = rel(0.8)),
      legend.title = element_text(size = rel(0.9)),
      plot.title = element_text(hjust = 0.5, face = "bold")
    )
}

# Standard colors for up/down regulation
VOLCANO_COLORS <- c("Down" = "#0072B2", "Not Sig" = "#CCCCCC", "Up" = "#D55E00")
```

## Code Templates

### Template 1: Volcano Plot with EnhancedVolcano

```r
library(EnhancedVolcano)

create_volcano <- function(de_results, filename = "volcano.pdf",
                            fc_cutoff = 1.0, p_cutoff = 0.05) {
  # de_results: data.frame with log2FoldChange, padj, gene (row names)

  p <- EnhancedVolcano(de_results,
    lab = rownames(de_results),
    x = 'log2FoldChange',
    y = 'padj',
    title = 'Differential Expression',
    subtitle = bquote(italic("Volcano Plot")),
    pCutoff = p_cutoff,
    FCcutoff = fc_cutoff,
    pointSize = 2.0,
    labSize = 3.5,
    labCol = 'black',
    labFace = 'bold',
    colCustom = NULL,
    colAlpha = 0.7,
    legendPosition = 'right',
    legendLabSize = 9,
    legendIconSize = 3.0,
    drawConnectors = TRUE,
    widthConnectors = 0.5,
    colConnectors = 'grey30',
    maxoverlapsConnectors = 20,
    # Shape by significance
    shape = c(1, 1, 19, 19),
    # Custom colors
    col = c('grey60', 'grey60', '#0072B2', '#D55E00'),
    # Border
    border = 'partial',
    borderWidth = 0.5,
    borderColour = 'black'
  )

  pdf(filename, width = 7, height = 5)
  print(p)
  dev.off()
  cat("Saved:", filename, "\n")
}

# Alternative: manual volcano plot for more control
create_volcano_manual <- function(de_df, fc_col = "log2FC", p_col = "padj",
                                   label_col = "gene", top_n = 15,
                                   filename = "volcano_manual.pdf") {
  de_df$significance <- "Not Sig"
  de_df$significance[de_df[[fc_col]] > 1 & de_df[[p_col]] < 0.05] <- "Up"
  de_df$significance[de_df[[fc_col]] < -1 & de_df[[p_col]] < 0.05] <- "Down"
  de_df$significance <- factor(de_df$significance,
                                levels = c("Down", "Not Sig", "Up"))

  # Select top genes to label
  top_genes <- de_df[order(de_df[[p_col]]), ][1:top_n, ]

  p <- ggplot(de_df, aes(x = .data[[fc_col]], y = -log10(.data[[p_col]]),
                          color = significance)) +
    geom_point(size = 1.5, alpha = 0.6) +
    scale_color_manual(values = VOLCANO_COLORS) +
    ggrepel::geom_text_repel(
      data = top_genes,
      aes(label = .data[[label_col]]),
      size = 3, max.overlaps = 20,
      segment.color = "grey50", segment.size = 0.3
    ) +
    geom_hline(yintercept = -log10(0.05), linetype = "dashed",
               color = "grey50", linewidth = 0.4) +
    geom_vline(xintercept = c(-1, 1), linetype = "dashed",
               color = "grey50", linewidth = 0.4) +
    labs(x = expression(log[2]~"Fold Change"),
         y = expression(-log[10]~italic("p-value")),
         color = "Regulation") +
    theme_bio() +
    theme(legend.position = "top")

  ggsave(filename, p, width = 6, height = 4.5, dpi = 600, device = cairo_pdf)
  cat("Saved:", filename, "\n")
}
```

### Template 2: Gene Expression Heatmap (ComplexHeatmap)

```r
library(ComplexHeatmap)
library(circlize)

create_expression_heatmap <- function(expr_matrix, annotation_df,
                                       top_n = 50, filename = "heatmap.pdf") {
  # expr_matrix: genes x samples
  # annotation_df: data.frame with sample annotations

  # Select top variable genes
  gene_vars <- apply(expr_matrix, 1, var)
  top_genes <- names(sort(gene_vars, decreasing = TRUE))[1:top_n]
  mat <- expr_matrix[top_genes, ]

  # Scale by row (z-score)
  mat_scaled <- t(scale(t(mat)))

  # Color function
  col_fun <- colorRamp2(c(-2, 0, 2), c("#0072B2", "white", "#D55E00"))

  # Annotation colors
  ha <- HeatmapAnnotation(
    df = annotation_df,
    col = list(
      Group = c("Control" = "#0072B2", "Treatment" = "#D55E00"),
      Batch = c("B1" = "#E69F00", "B2" = "#009E73")
    ),
    annotation_name_side = "left",
    annotation_name_gp = gpar(fontsize = 9),
    annotation_legend_param = list(
      title_gp = gpar(fontsize = 9),
      labels_gp = gpar(fontsize = 8)
    )
  )

  # Draw heatmap
  pdf(filename, width = 8, height = 10)
  ht <- Heatmap(mat_scaled,
    name = "Z-score",
    col = col_fun,
    top_annotation = ha,
    show_row_names = TRUE,
    row_names_gp = gpar(fontsize = 6),
    show_column_names = TRUE,
    column_names_gp = gpar(fontsize = 8),
    clustering_method_rows = "ward.D2",
    clustering_method_columns = "ward.D2",
    row_title = "Genes",
    column_title = "Gene Expression Heatmap",
    column_title_gp = gpar(fontsize = 11, fontface = "bold"),
    heatmap_legend_param = list(
      title_gp = gpar(fontsize = 9),
      labels_gp = gpar(fontsize = 8)
    )
  )
  draw(ht)
  dev.off()
  cat("Saved:", filename, "\n")
}
```

### Template 3: Sankey / Alluvial Diagram

```r
library(ggalluvial)

create_sankey <- function(flow_data, filename = "sankey.pdf") {
  # flow_data: data.frame with axis1, axis2, axis3, freq columns

  p <- ggplot(flow_data,
              aes(axis1 = axis1, axis2 = axis2, axis3 = axis3, y = freq)) +
    geom_alluvium(aes(fill = axis1), width = 1/6, alpha = 0.7,
                  curve_type = "arctangent") +
    geom_stratum(width = 1/6, fill = "grey90", color = "grey40",
                 linewidth = 0.3) +
    geom_text(stat = "stratum", aes(label = after_stat(stratum)),
              size = 3) +
    scale_fill_brewer(palette = "Set2") +
    scale_x_discrete(limits = c("Stage 1", "Stage 2", "Stage 3"),
                     expand = c(0.15, 0.05)) +
    labs(y = "Count", fill = "Category") +
    theme_bio() +
    theme(
      axis.text.y = element_blank(),
      axis.title.y = element_blank(),
      panel.grid = element_blank()
    )

  ggsave(filename, p, width = 7, height = 5, dpi = 600, device = cairo_pdf)
  cat("Saved:", filename, "\n")
}

# Usage
flow <- data.frame(
  axis1 = sample(c("Gene A", "Gene B", "Gene C"), 100, replace = TRUE),
  axis2 = sample(c("Pathway 1", "Pathway 2"), 100, replace = TRUE),
  axis3 = sample(c("Phenotype X", "Phenotype Y", "Phenotype Z"), 100, replace = TRUE),
  freq = sample(5:20, 100, replace = TRUE)
)
```

### Template 4: GO Enrichment Dot Plot

```r
library(clusterProfiler)

create_enrichment_plot <- function(enrichment_df, top_n = 15,
                                    filename = "go_enrichment.pdf") {
  # enrichment_df: data.frame with Description, p.adjust, Count, GeneRatio

  enrichment_df <- enrichment_df[order(enrichment_df$p.adjust), ][1:top_n, ]
  enrichment_df$Description <- factor(enrichment_df$Description,
                                       levels = rev(enrichment_df$Description))

  p <- ggplot(enrichment_df, aes(x = GeneRatio, y = Description,
                                  size = Count, color = p.adjust)) +
    geom_point(alpha = 0.8) +
    scale_color_viridis_c(direction = -1, option = "plasma") +
    scale_size_continuous(range = c(3, 10)) +
    labs(x = "Gene Ratio", y = "", color = "Adjusted p-value",
         size = "Gene Count") +
    theme_bio() +
    theme(
      axis.text.y = element_text(size = 8),
      legend.position = "right"
    )

  ggsave(filename, p, width = 8, height = max(4, top_n * 0.35),
         dpi = 600, device = cairo_pdf)
  cat("Saved:", filename, "\n")
}
```

## Style Specifications

| Element | Value |
|---------|-------|
| Up-regulated color | #D55E00 (red-orange) |
| Down-regulated color | #0072B2 (blue) |
| Non-significant | #CCCCCC (light gray) |
| Font family | sans (Helvetica/Arial) |
| Point size (volcano) | 1.5–2.5 |
| Label font size | 3–4 pt |
| Heatmap cell border | 0.3 pt, white |
| Dendrogram line width | 0.6 pt |

## Common Pitfalls

1. **Volcano plot labels overlapping**: Use `ggrepel` with `max.overlaps = 20`
2. **Heatmap scaling wrong**: Always z-score by row, not column, for gene comparisons
3. **P-value cutoff confusion**: Use adjusted p-value (`padj`), not raw p-value
4. **Sankey diagram ordering**: Factor levels define left-to-right order
5. **GO enrichment redundancy**: Remove redundant GO terms before plotting
6. **ComplexHeatmap annotation alignment**: Ensure annotation order matches column order
7. **Missing `dev.off()` in base graphics**: Always close device after `pdf()`/`png()`

## Journal-Specific Tips

- **Nature Genetics**: Prefer ComplexHeatmap; provide raw count matrix as supplement
- **Genome Biology**: Open access; provide full analysis code in GitHub
- **NAR**: Minimum 300 DPI; vector preferred for diagrams
- **Cell Systems**: Support wide figures; interactive supplements encouraged
- **General**: Always specify log2 fold change direction; use adjusted p-values; describe statistical methods in figure legend
