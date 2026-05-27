# 01-clean.R
# Purpose: Load raw data, apply exclusion criteria, compute scale scores, merge
# Input:   data/raw/employee_survey.csv, data/raw/supervisor_survey.csv
# Output:  data/cleaned/study_data.csv

if (!require("tidyverse")) install.packages("tidyverse")
library(tidyverse)

# ── 1. Load ────────────────────────────────────────────────────────────────────

data_employees <- read_csv("data/raw/employee_survey.csv")
data_supervisors <- read_csv("data/raw/supervisor_survey.csv")

cat("\nRaw employee rows:", nrow(data_employees))
cat("\nRaw supervisor rows:", nrow(data_supervisors), "\n")

# ── 2. Exclude failed attention checks ─────────────────────────────────────────

data_employees <- data_employees |>
  filter(attn_check == 4)

cat("\nAfter attention check exclusion:", nrow(data_employees), "employees retained\n")

# ── 3. Compute scale scores ───────────────────────────────────────────────────

# Reverse-score js3 (1→5, 2→4, 3→3, 4→2, 5→1), then average items via rowMeans
data_employees <- data_employees |>
  mutate(
    js3r      = 6 - js3,
    js_score  = rowMeans(pick(js1, js2, js3r), na.rm = TRUE),
    eng_score = rowMeans(pick(eng1, eng2, eng3), na.rm = TRUE)
  )

data_supervisors <- data_supervisors |>
  mutate(
    perf_score = rowMeans(pick(perf1, perf2, perf3), na.rm = TRUE),
    ocb_score  = rowMeans(pick(ocb1, ocb2), na.rm = TRUE)
  )

# ── 4. Merge employee and supervisor data ─────────────────────────────────────

study_data <- data_employees |>
  inner_join(data_supervisors, by = "emp_id")

cat("Merged observations:", nrow(study_data), "\n\n")

# ── 5. Export ──────────────────────────────────────────────────────────────────

dir.create("data/cleaned", showWarnings = FALSE)
write_csv(study_data, "data/cleaned/data_merge.csv")

cat("Cleaned data written to data/cleaned/data_merge.csv\n")
