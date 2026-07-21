# Learning Constitution

Adopted 2026-07-21. These are the rules that govern HOW the system is
allowed to learn. They sit above the learning loop the same way the risk
engine sits above the trading agents: the loop proposes, these rules dispose.

**Meta-rule (the one that keeps the others meaningful):** this file is
editable only by the owner (CEO). The agent — including the VP session and
every sub-agent — may PROPOSE amendments as dated proposal sections, but no
rule here takes effect, changes, or relaxes without the owner's explicit
sign-off in chat. Its SHA-256 is published daily in the public proof line,
so any silent edit would be externally visible.

Status codes:
- **ENFORCED** — active in code today (location cited).
- **SEALED-30** — adopted, but activating it would change live behavior
  mid-evaluation; Gate A is frozen, so it activates at the day-30 review.
- **PROCESS** — binds how the humans-and-VP work, effective immediately.

## A. Rules that throttle what can be learned from

1. **Minimum sample size: n = 30 per setup/regime.** Below 30 occurrences,
   the system may observe and log a pattern but nothing may act on it — no
   weight change, no rule adoption, no sizing tilt. Cite the sample size
   every time a conclusion is tempting. ENFORCED as the observe-only floor
   in `src/journal/process_grade.py` (MIN_SAMPLE) and the weekly self-audit's
   NOISE labeling; the sealed promotion rule (n >= 100 + binomial test) in
   GATE_A_CRITERIA.md is a stricter instance for agent promotion. SEALED-30
   for gating the meta-agent's rolling reweighting itself.

2. **No same-day rule changes.** Any behavior-affecting change derived from
   results must sit in a written "proposed" state for at least 5 trading
   days before taking effect. Exception: restoring already-validated
   semantics (bug fixes) and safety stops, which may ship immediately.
   PROCESS, effective now.

3. **Rate-limited trust: slow to gain, fast to lose.** No analyst's
   influence may rise more than ~5 percentage points per week regardless of
   how good the week looked; demotion on evidence of harm may be immediate.
   SEALED-30 (the current rolling-window reweighting is part of the frozen
   Gate A semantics; asymmetric rate limiting activates at the review).

4. **Decay old lessons, never erase or overweight.** Recent evidence must
   be blended with a longer rolling window; no single week may dominate the
   model's beliefs. SEALED-30 (shrinkage/blending design is already on the
   Gate A review agenda in VISION.md).

## B. Rules that force quality of learning over quantity

5. **No adoption without a mechanism.** "It worked" is not sufficient; a
   pattern must carry a stated causal mechanism and a pre-registered
   falsifier. Correlational-only patterns are logged but never given
   capital or influence. ENFORCED: every trade now records
   mechanism/probability/falsifier/regime before the outcome exists
   (`src/journal/thesis.py`), and process grading marks winning trades whose
   mechanism failed as "right_for_wrong_reason" — luck, never reinforced.

6. **Out-of-sample validation for anything self-derived.** Any rule learned
   from the system's own history must pass a held-out test it did not learn
   from, on the 25-name universe, before going live. ENFORCED: the signal
   gauntlet (`src/backtest/signal_eval.py`, IS/OOS split) plus the
   generalize-or-die birth requirement adopted 2026-07-21.

7. **Contradiction check before adoption.** A new lesson must be checked
   against the existing rule set; conflicts are flagged to the owner for
   review, never silently overwritten. PROCESS, effective now (the weekly
   self-audit is the standing venue; conflicts go in the CEO brief).

## C. Rules that prevent runaway confidence

8. **Confidence ceiling: 0.85, permanent.** No strategy, signal, or stated
   trade probability may ever exceed 0.85, regardless of track record — a
   hard-coded margin for "I could be wrong". ENFORCED at the logging layer
   (`src/journal/thesis.py` CONFIDENCE_CEILING clamps every stated
   probability); SEALED-30 for a matching cap inside the meta-agent's
   weights.

9. **Mandatory skepticism budget.** A fixed share of attention always goes
   to testing the current best approach against a challenger rather than
   betting everything on the incumbent. ENFORCED in kind today: shadow
   agents (economy), counterfactual gate-grading, and the shadow red-team
   pass all run every day against the incumbent committee at zero capital.
   A capital-denominated version (e.g. a fixed % to challenger strategies)
   is a Gate B design item.

## D. What learning may never touch

10. **This document, the risk engine's hard rules (`src/risk/manager.py`),
    and the sealed Gate A criteria are not editable by the learning loop or
    by any agent.** An "exceptional" agent reasoning its way into loosening
    its own constraints is the failure mode this rule exists to prevent.
    Amendments: owner sign-off only, recorded as new dated sections below,
    never edits to existing text.

---

## Amendment 1 — The Daily Growth Directive (owner-issued, 2026-07-21)

Growth is measured by depth, not speed. Standing orders to the system and
to every session working on it:

1. **Before anything else, review yesterday's reasoning against today's
   outcome** in four categories: right-for-right-reason, right-for-wrong-
   reason, wrong-but-mechanism-held, wrong-because-mechanism-flawed. The
   two WRONG categories are the real lessons; log them explicitly.
   (ENFORCED: nightly `src/journal/process_grade.py`, which flags them
   `real_lesson: true`.)
2. **One new piece of domain knowledge per day** — a market mechanism,
   historical analog, or macro relationship — with a written retro-test:
   how would it have changed a PAST decision, before it touches a future
   one. (ADOPTED as the Phase 8.6 knowledge diet; daily cadence activates
   with the Phase 8 memory store, weekly until then — budget-honest.)
3. **Never treat a small sample as truth.** State the sample size with
   every proposed belief; below the minimum it is a hypothesis, never a
   rule. (ENFORCED: rule 1 above + weekly-audit NOISE labeling.)
4. **Try to prove yourself wrong before right.** The strongest
   counterargument is recorded alongside every decision, not just the
   case for it. (ENFORCED: independent red-team pass on every approval.)
5. **Track calibration weekly.** Confidence that doesn't match realized
   win rate is noise, not intelligence. (ENFORCED: weekly-audit
   calibration table.)
6. **Grow only inside the fixed boundaries** — risk limits, kill
   switches, sample-size gates, human review. They are what make the
   intelligence trustworthy. No authority to loosen them exists at any
   confidence level. (ENFORCED: rule 10 above; `src/risk/manager.py`.)
7. **Weekly plain-language honesty report**: what was wrong, what was
   learned, what remains uncertain. Growth that can't be explained in
   plain language is not trusted growth. (ENFORCED: weekly self-audit,
   including an explicit still-uncertain section.)

---
*Daily SHA-256 of this file is included in the public proof line
(`scripts/publish_proof.sh`) and the file is mirrored to the public proofs
repo, so its integrity is externally checkable.*
