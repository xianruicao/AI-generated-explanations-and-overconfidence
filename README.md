# Results Summary

## Analysis file
This project now uses a single notebook as the full analysis workflow:
- `clean_data_groups.ipynb`

The notebook contains the full process:
- raw data loading
- cleaning decisions and sample filtering
- group splitting
- descriptive statistics
- figure creation
- H1 confidence tests
- H2 objective scoring
- H2b stability check using `Q5` and `Q86`
- H3 overconfidence-gap analysis using `Q13_1` against `Q10`, `Q84`, `Q11`, and `Q86`

## Research question
This project tests whether a well-structured AI explanation increases perceived understanding more than it improves actual transferable understanding.

## Sample and inclusion rule
The current analysis uses the export:
- `Why+do+AI+explanations+feel+like+understanding__March+28,+2026_09.32.csv`

Responses were included only if they met all of the following conditions:
- `StartDate > 2026-03-05 19:28:00`
- `Finished = True`
- `Progress = 100`
- `GroupA` = `Group1` filled and `Group2` empty
- `GroupB` = `Group2` filled and `Group1` empty

Final sample:
- `GroupA`: 85 complete responses
- `GroupB`: 85 complete responses
- Total: 170 complete responses


## Key measures
- `P_Knowl` (`Q2`) = "Before today, how much did you know about how antibiotics work and why they sometimes stop working?"
- `R_con` (`Q4`) = "How confident are you that you understood the explanation you just read?"
- `Q_con` (`Q7`) = "How confident are you regarding your responses to the previous questions?"
- `No./4` (`Q13_1`) = "Of the 4 questions related to antibiotics and resistance, how many do you think you answered correctly?"

Group labels:
- `GroupA` = AI / fluent condition
- `GroupB` = non-AI control / disfluent condition

## H1: Perceived understanding and confidence
H1 is reported as two related sub-hypotheses rather than a single pooled outcome.

- `H1a`: the AI condition increases immediate comprehension confidence after reading (`R_con`)
- `H1b`: the AI condition increases confidence in one's answers after responding (`Q_con`)

Descriptive pattern:
- `R_con`
  - GroupA: mean `7.6000`, median `8.0`, mode `10.0`
  - GroupB: mean `6.9176`, median `7.0`, mode `8.0`
- `Q_con`
  - GroupA: mean `6.9882`, median `7.0`, mode `10.0`
  - GroupB: mean `6.4706`, median `7.0`, mode `8.0`

Inferential results:
- `H1a / R_con`: mean difference `+0.6824`, 95% CI `[-0.0205, 1.3852]`, Welch `p = 0.0570`, Cohen's `d = 0.2940`
- `H1b / Q_con`: mean difference `+0.5176`, 95% CI `[-0.2322, 1.2675]`, Welch `p = 0.1748`, Cohen's `d = 0.2090`

Supplementary composite:
- `Perceived_Understanding = (R_con + Q_con) / 2`: mean difference `+0.6000`, 95% CI `[-0.0793, 1.2793]`, Welch `p = 0.0830`, Cohen's `d = 0.2675`

Interpretation:
- Both confidence outcomes move in the predicted direction, with GroupA higher than GroupB.
- The evidence is stronger for `R_con` than for `Q_con`.
- `R_con` is marginal at the `0.10` level but is not conventionally significant at `0.05`.
- `Q_con` is descriptively higher in GroupA, but the statistical evidence is weaker.
- The combined `Perceived_Understanding` score also moved in the predicted direction, with GroupA higher than GroupB, but the composite difference remained non-significant at the `0.05` level (`p = 0.0830`).

## H2a: Transfer understanding
The main transfer analysis uses `Q10`, `Q84`, and `Q11`.

These three items are treated as the core transfer measure because they ask participants to apply the resistance logic to the pesticide case, which is a new domain.

Main result:
- `Q10`: GroupA `12.94%`, GroupB `11.76%`, `p = 0.8157`
- `Q84`: GroupA `24.71%`, GroupB `35.29%`, `p = 0.1320`
- `Q11`: GroupA `36.47%`, GroupB `34.12%`, `p = 0.7482`
- GroupA transfer mean: `0.7412 / 3` (`24.71%`)
- GroupB transfer mean: `0.8118 / 3` (`27.06%`)
- Welch test for transfer total: `p = 0.5949`
- Mann-Whitney test for transfer total: `p = 0.8625`

Regression result:
- `Q2` coefficient: `-0.0057`, `p = 0.7990`
- `GroupA` coefficient: `-0.0694`, `p = 0.6020`
- `R^2 = 0.0021`

Interpretation:
- The results are consistent with H2a: transfer understanding did not differ significantly between conditions.
- Descriptively, the control/disfluent group performed slightly better on the transfer score, which also matches the predicted direction of H2.
- This should be described as support for H2a in the present sample, not as proof that the two conditions are truly equivalent.
- A regression model (`transfer_total ~ Q2 + group`) showed that neither prior knowledge nor group assignment significantly predicted transfer performance (`Q2: p = .7990`, `GroupA: p = .6020`, `R^2 = .0021`). This is consistent with H2a.

## H2b: Stability of objective understanding (`Q5` vs `Q86`)
`Q5` and `Q86` ask the same antibiotic-resistance concept at two different points in the survey, so they can be used as a short-term stability check rather than as independent knowledge items.

Main result:
- GroupA: `Q5 = 85.88%`, `Q86 = 70.59%`, change `-15.29` percentage points
- GroupB: `Q5 = 77.65%`, `Q86 = 67.06%`, change `-10.59` percentage points
- Within-group McNemar test: GroupA `p = 0.0089`, GroupB `p = 0.0703`
- Between-group difference in change: GroupA mean change `-0.1529`, GroupB mean change `-0.1059`, Welch `p = 0.4765`

Interpretation:
- Both groups performed worse when the same concept reappeared later in the survey.
- Descriptively, the drop was larger in GroupA than in GroupB.
- The between-group difference in decline was not significant, so H2b should be treated as suggestive rather than conclusive in the present sample.

## H3: The overconfidence gap
H3 is tested with the self-estimated four-item score in `Q13_1`.

This is the preferred H3 algorithm because the self-estimate and the actual score refer to the same four questions:
- self-estimated rate = `Q13_1 / 4`
- actual four-item rate = `(Q10_correct + Q84_correct + Q11_correct + Q86_correct) / 4`
- overconfidence gap = `self-estimated rate - actual four-item rate`

Main result:
- GroupA: self-estimated rate `0.7706`, actual four-item rate `0.3618`, gap `0.4088`
- GroupB: self-estimated rate `0.7471`, actual four-item rate `0.3706`, gap `0.3765`
- Between-group Welch test for the gap: `p = 0.4839`
- Between-group Mann-Whitney test for the gap: `p = 0.6182`
- Within-group one-sample tests against zero: both groups `p < 0.001`

Interpretation:
- Both groups substantially overestimated how many of the four items they answered correctly.
- Descriptively, the overconfidence gap was larger in GroupA than in GroupB.
- The observed direction is consistent with H3: GroupA showed a larger overconfidence gap than GroupB, but the between-group difference was not statistically significant.

## Comparison with the previous working sample
- Previous working sample: 156 post-cutoff grouped responses
- Previous group counts: 77 in GroupA and 79 in GroupB
- Current complete sample: 170 responses
- Current group counts: 85 in GroupA and 85 in GroupB
- Net increase: 14 complete grouped responses
- The directional pattern did not reverse
- The main change is that the `R_con` result moved from `p = 0.0478` in the earlier sample to `p = 0.0570` in the refreshed complete sample
