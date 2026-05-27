# Codebook: Employee–Supervisor Survey Study

**Principal Investigator:** Don Zhang
**Data collection:** Spring 2024
**Sample:** Full-time employees and their direct supervisors at a mid-sized U.S. organization
**Design:** Two-source, time-lagged survey. Employees completed a self-report survey (Time 1); supervisors independently rated each direct report (Time 2, approximately 2 weeks later).
**Files:** `employee_survey.csv` (n = 150), `supervisor_survey.csv` (n = 150)
**Linking key:** `emp_id` (present in both files)

---

## File 1: Employee Survey (`employee_survey.csv`)

### Demographics & Identifiers

| Variable | Label | Type | Values / Range |
|---|---|---|---|
| `emp_id` | Employee ID | string | E001–E150 |
| `age` | Age | integer | 22–62 (years) |
| `gender` | Gender identity | integer | 1 = Man, 2 = Woman, 3 = Non-binary / prefer not to say |
| `tenure` | Organizational tenure | numeric | 0.5–20.0 (years) |
| `department` | Department | integer | 1 = Sales, 2 = Operations, 3 = Human Resources, 4 = Finance |

### Data Quality

| Variable | Label | Type | Values / Range | Item wording |
|---|---|---|---|---|
| `attn_check` | Attention check | integer | 1–5 | "As a quality check, please select '4 – Agree' for this item." |

*Correct response:* 4. Respondents with `attn_check ≠ 4` should be excluded prior to analysis.

### Job Satisfaction Scale

*Response scale:* 1 = Strongly Disagree, 2 = Disagree, 3 = Neutral, 4 = Agree, 5 = Strongly Agree

| Variable | Label | Type | Values | Item wording | Scoring |
|---|---|---|---|---|---|
| `js1` | Job satisfaction 1 | integer | 1–5 | "I am satisfied with my job overall." | Standard |
| `js2` | Job satisfaction 2 | integer | 1–5 | "I find my work meaningful." | Standard |
| `js3` | Job satisfaction 3 | integer | 1–5 | "I often feel like quitting my job." | **Reverse-scored** |

*Scale score:* `js_score = mean(js1, js2, 6 − js3)`. Higher scores = greater job satisfaction.

### Work Engagement Scale

*Response scale:* 1 = Strongly Disagree, 2 = Disagree, 3 = Neutral, 4 = Agree, 5 = Strongly Agree

| Variable | Label | Type | Values | Item wording | Scoring |
|---|---|---|---|---|---|
| `eng1` | Work engagement 1 | integer | 1–5 | "I feel energetic at work." | Standard |
| `eng2` | Work engagement 2 | integer | 1–5 | "I am enthusiastic about my job." | Standard |
| `eng3` | Work engagement 3 | integer | 1–5 | "I am fully absorbed in my work." | Standard |

*Scale score:* `eng_score = mean(eng1, eng2, eng3)`. Higher scores = greater engagement.

---

## File 2: Supervisor Survey (`supervisor_survey.csv`)

### Identifiers

| Variable | Label | Type | Values / Range |
|---|---|---|---|
| `sup_id` | Supervisor ID | string | S01–S25 |
| `emp_id` | Employee ID | string | E001–E150 |

*Each supervisor rated an average of 6 direct reports. `emp_id` links supervisor ratings to employee self-reports.*

### Task Performance Scale

*Response scale:* 1 = Not at all characteristic, 2 = Slightly characteristic, 3 = Moderately characteristic, 4 = Very characteristic, 5 = Extremely characteristic

| Variable | Label | Type | Values | Item wording | Scoring |
|---|---|---|---|---|---|
| `perf1` | Task performance 1 | integer | 1–5 | "This employee completes tasks on time." | Standard |
| `perf2` | Task performance 2 | integer | 1–5 | "This employee meets quality standards." | Standard |
| `perf3` | Task performance 3 | integer | 1–5 | "This employee consistently exceeds expectations." | Standard |

*Scale score:* `perf_score = mean(perf1, perf2, perf3)`. Higher scores = better performance.

### Organizational Citizenship Behavior (OCB) Scale

*Response scale:* 1 = Not at all characteristic, 2 = Slightly characteristic, 3 = Moderately characteristic, 4 = Very characteristic, 5 = Extremely characteristic

| Variable | Label | Type | Values | Item wording | Scoring |
|---|---|---|---|---|---|
| `ocb1` | OCB 1 | integer | 1–5 | "This employee helps coworkers without being asked." | Standard |
| `ocb2` | OCB 2 | integer | 1–5 | "This employee volunteers for tasks beyond their role." | Standard |

*Scale score:* `ocb_score = mean(ocb1, ocb2)`. Higher scores = more citizenship behavior.

---

## Missing Data

Approximately 5% of scale item responses are missing (NA), distributed randomly across `js1`–`js3` and `eng1`–`eng3`. Use `na.rm = TRUE` when computing scale means, or apply listwise/pairwise exclusion as appropriate for the analysis.

---

## Nested Structure

Employees are nested within supervisors (Level 1: employees; Level 2: supervisors). If running multilevel models, specify `sup_id` as the grouping variable.
