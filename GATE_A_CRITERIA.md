# GATE A — PRE-REGISTERED CRITERIA (sealed before results exist)

Committed on day 4 of ~30. This document may NOT be edited after commit;
any amendment requires a new dated section BELOW, never a rewrite, and the
git history is the proof. Internal mandate: pursue best risk-adjusted
returns. Public claim: only what this pre-registered process can prove.

## Primary metric
Net R after modeled costs, REAL executed phantom/paper trades only
(counterfactuals excluded from the metric; they grade the gate separately).

## Day 1 ruling (decided by PRINCIPLE, before the outcome is known to help or hurt)
Day 1 (2026-07-16) ran pre-fix re-entry semantics — different code than
what is being evaluated. RULE: only trades executed under the frozen,
churn-fixed semantics count. Day 1 is EXCLUDED from the primary metric
(reported alongside for transparency). NOTE RECORDED AT SEALING: this
exclusion currently HURTS the result (removes +5.0R, leaving the running
primary metric at -3.11R as of sealing) — accepted anyway, because the
rule is principled, not curve-fit.

## Verdict rules at day 30 (evaluated on days 2–30 real trades)
- PASS requires ALL of:
  (a) n >= 25 executed trades
  (b) net R > 0 after costs
  (c) beats buy-and-hold SPY (same window, R-equivalent at our risk unit)
  (d) beats the 95th percentile of >= 1,000 matched random-entry
      simulations (same exits, risk caps, cost model)
  (e) zero risk-rule violations during the window
- FAIL: n >= 25 AND net R < 0 after costs.
- INCONCLUSIVE: anything else (including n < 25). Pre-committed response:
  Gate A2 — extend 30 more trading days with IDENTICAL frozen code. No
  tweak-and-rerun. Ever.

## Statistical honesty (stated in advance)
The active signal's backtest edge (+0.256R) requires on the order of ~550
trades for conventional 95% confirmation. THIRTY DAYS CANNOT CONFIRM AN
EDGE THIS SMALL. Gate A can reject a bad system or return
inconclusive-but-promising; it cannot certify success. Confidence
intervals via bootstrap (10,000 resamples), not t-tests. The active signal
survived selection from 6 candidates — its backtest is selection-biased
upward and Gate A is framed as its second, cleaner OOS test. Report the
distribution: max drawdown (R), longest losing streak, % of net R from the
single best trade.

## Baselines (to be coded and frozen before day 30)
1. Buy-and-hold SPY, same window
2. Matched random-entry distribution (>=1,000 runs; same exits/costs/caps)
3. Always-abstain (0R)
Gate/abstention verdict held to the same bar: no "the gate works" claim
before n >= 50 resolved counterfactuals; same statistical treatment.

## Cost model floor (already live) + sensitivity
1bp/side slippage parity minimum; results additionally reported at 0.5x,
1x, 2x modeled costs. If the edge dies at 2x, it is too fragile to deploy.

## Freeze list (contractual until the verdict)
Active signals, confluence rule, sizing, risk limits, universe. Frozen.
Regime gating, correlation caps, dynamic sizing, promotions: Gate A agenda
only. Permitted during the run: ops/monitoring/backup fixes, shadow-mode
additions (zero vote), data-capture additions — each logged in git.

## Run invalidators
- Any manual intervention in live trading decisions
- Any mid-run change to trading semantics in src/ (ops exempt, logged)
- Data outage losing more than one full trading day
If invalidated: restart the window. No partial credit.

## Agent promotion rule (pre-registered)
No shadow agent is promoted before: n >= 100 graded calls AND a binomial
test against the actual market base rate of its call directions (not
against 50%) at p < 0.05. Weight updates use shrinkage toward the equal-
weight prior. Small-sample hot streaks (e.g. "65% of 20") are noise until
this bar is met.
