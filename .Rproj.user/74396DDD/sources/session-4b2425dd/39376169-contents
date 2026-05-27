# 04-regression.R
# Purpose: Predict supervisor-rated performance from employee engagement
#          and job satisfaction
# Input:   data/cleaned/data_merge.csv

if (!require("tidyverse")) install.packages("tidyverse")
library(tidyverse)

data_merge <- read_csv("data/cleaned/data_merge.csv")

# ── 1. Simple regression ───────────────────────────────────────────────────────

model_1 <- lm(perf_score ~ eng_score + js_score, data = data_merge)

cat("\n========== Regression: perf_score ~ eng_score + js_score ==========\n")
summary(model_1)
