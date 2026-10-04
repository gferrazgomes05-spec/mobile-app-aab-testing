# Mobile App Funnel & A/A/B Testing

An analysis of event participation and a font-design experiment in a food retail mobile app.

## Business question

Where does user participation fall across the purchase funnel, and is there evidence that a font change affects event participation?

## Key findings

- **7,534 users and 240,887 events** in the selected period, August 1–7, 2019, after deduplication and removal of incomplete earlier records.
- The largest event-reach gap is between the main screen (**7,419 users**) and the offers screen (**4,593 users**). Offers reach is **61.91%** of main-screen reach.
- **3,539 users** generated a successful-payment event: **46.97%** of all observed users. Payment reach is **47.70%** of main-screen reach.
- One comparison has an unadjusted p-value below 0.10 (cart participation, groups 246 vs. 248; **p ≈ 0.0784**). **None of the 20 comparisons is significant at the Bonferroni threshold of 0.005.**

**Recommendation:** Investigate navigation and event instrumentation between the main and offers screens. The experiment does not establish a conversion benefit from the font change; absence of statistical significance does not establish equivalence or absence of harm.

## Approach

1. Inspect event data, remove 413 duplicate rows, and convert Unix timestamps.
2. Select the period with consistent event coverage.
3. Count unique users per event and compare aggregate funnel-stage reach.
4. Compare two control groups (246, 247), then the font variant (248) against each control and their pooled sample.
5. Use two-sided tests for proportions and account for 20 distinct comparisons with Bonferroni correction.

## Read the analysis

[Open the notebook](analysis.ipynb)

**Tools:** Python, Pandas, NumPy, Matplotlib, SciPy, Jupyter.

## Interpretation and limitations

- Funnel ratios compare unique-user counts per event. They do not verify that the same users completed events in chronological order, so they are not sequential conversion probabilities.
- The A/A comparison is a diagnostic check, not proof of valid randomization or equivalent groups.
- The 87.84% false-positive illustration in the notebook assumes independent tests and all null hypotheses true. The actual comparisons share users and events, so that figure is not an estimate of this experiment's exact error rate. Bonferroni does not require independence.
- Findings apply to this educational dataset and its observation window. The analysis does not establish causal explanations for funnel gaps or quantify the smallest detectable effect.

## Run locally

Use Python 3 in an isolated environment, then install the dependencies:

```bash
pip install -r requirements.txt
jupyter lab
```

Place the tab-separated `logs_exp_us.csv` in `data/`, open `analysis.ipynb`, and run all cells from the repository directory. The required columns are documented in [DATA.md](DATA.md).

The source dataset is not included. Obtain it through authorized TripleTen course access.

## Provenance and validation

Analysis by Gabriella Ferraz Gomes, developed during the TripleTen Data Analytics bootcamp. This portfolio edition preserves the analytical approach, with editorial clarification of statistical thresholds and funnel interpretation. Outputs were regenerated using the supplied source CSV.

All 45 code cells were executed in order in a fresh IPython process with Python 3.13. The run completed without errors or cell warnings. Checks confirmed 240,887 events, 7,534 users, and no users assigned to multiple experimental groups in the retained period. Headline funnel ratios and the 20 statistical comparisons were also checked. Package versions for the execution environment are recorded in `requirements.txt`.
