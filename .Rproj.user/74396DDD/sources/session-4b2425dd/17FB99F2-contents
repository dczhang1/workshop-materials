# 03-correlation.R
# Purpose: Publication-quality correlation matrix with scatter plots
# Input:   data/cleaned/data_merge.csv
# Output:  figures/correlation_plot.png

if (!require("tidyverse")) install.packages("tidyverse")
library(tidyverse)
if (!require("corrplot")) install.packages("corrplot")
library(corrplot)
if (!require("RColorBrewer")) install.packages("RColorBrewer")
library(RColorBrewer)

data_merge <- read_csv("data/cleaned/data_merge.csv")

# ── 1. Compute correlation matrix ──────────────────────────────────────────────

vars <- data_merge |>
  select(js_score, eng_score, perf_score, ocb_score)

cor_matrix <- cor(vars, use = "pairwise.complete.obs")

cat("========== Correlation matrix ==========\n")
print(round(cor_matrix, 2))

# ── 2. Plot ────────────────────────────────────────────────────────────────────

dir.create("figures", showWarnings = FALSE)

png("figures/correlation_plot.png",
    width  = 6,
    height = 6,
    units  = "in",
    res    = 300)

corrplot(cor_matrix,
         method      = "color",
         type        = "upper",
         order       = "original",
         tl.col      = "black",
         tl.cex      = 0.9,
         addCoef.col = "black",
         number.cex  = 0.8,
         col         = brewer.pal(n = 8, name = "RdYlBu"),
         mar         = c(1, 1, 2, 1),
         title       = "Correlation Plot (N = 135)")

dev.off()

cat("\nPlot saved to figures/correlation_plot.png\n")
