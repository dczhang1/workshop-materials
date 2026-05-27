# 02-describe.R
# Purpose: Descriptive statistics for the cleaned study data
# Input:   data/cleaned/data_merge.csv

if (!require("tidyverse")) install.packages("tidyverse")
library(tidyverse)
if (!require("psych")) install.packages("psych")
library(psych)

data_merge <- read_csv("data/cleaned/data_merge.csv")

# ── 1. Demographics ────────────────────────────────────────────────────────────

cat("========== Demographics ==========\n")

data_merge |>
  summarise(
    n            = n(),
    age_mean     = mean(age, na.rm = TRUE),
    age_sd       = sd(age, na.rm = TRUE),
    tenure_mean  = mean(tenure, na.rm = TRUE),
    tenure_sd    = sd(tenure, na.rm = TRUE)
  ) |>
  print()

cat("\nGender distribution:\n")
data_merge |>
  count(gender) |>
  mutate(pct = n / sum(n) * 100) |>
  print()

cat("\nDepartment distribution:\n")
data_merge |>
  count(department) |>
  mutate(pct = n / sum(n) * 100) |>
  print()

# ── 2. Describe key variables ─────────────────────────────────────────────────

cat("\n========== Scale descriptives ==========\n")
describe(data_merge |>
           select(js_score, eng_score, perf_score, ocb_score))

# ── 3. Describe individual items ──────────────────────────────────────────────

cat("\n========== Job satisfaction items ==========\n")
describe(data_merge |> select(js1, js2, js3))

cat("\n========== Engagement items ==========\n")
describe(data_merge |> select(eng1, eng2, eng3))

cat("\n========== Performance items ==========\n")
describe(data_merge |> select(perf1, perf2, perf3))
