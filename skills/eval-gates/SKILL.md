---
name: eval-gates
description: Gate anything a model writes or judges with evals that have fixed pass marks, held-out cases and a spending cap. Use when adding or changing a prompt, a model, an agent, a judge, or code that changes what a model is sent, when switching on or off a step that feeds a model, and before shipping any AI feature.
---

# Eval gates

A change to what a model reads or writes ships only after its evals pass. The numbers must be true, and the pass
marks do not move. Evals judge what a model writes. The code around it (the harness, parsers, gates) is tested like
any other code, by the agreement's Tests rules, and never calls a model for real in a test.

## Before any run

- Fix the pass marks first. Never propose them from a run's results, and never move one after a miss.
- Set a spending cap with the owner, and a stop line a little under it. State the spend so far and the projection
  before each run.
- Build cases from real inputs, run through the production path, with what production will have on day one. If a
  step is switched off or parked, measure everything downstream without its output.
- Before the first paid run, print one case's full request beside the request production builds for the same record.
  Every difference is fixed or named in the record.
- Labels come from two independent judges and a tie-breaker. Each judge works alone, without the key or the
  other's answers. A model that judges inside an eval answers three times, and the majority counts.

## The three sets

1. **Tuning set.** Read its misses freely and tune until every mark is met.
2. **Held-out set.** A gate. Read totals only.
3. **Fresh batch.** New cases, judged the same way, run once. This is the number of record.

Count the runs of a held-out set and quote the count with its number. Once its misses have been read, or the code
has changed because of its totals, call it seen, never unseen. The record is always a fresh batch.

## A miss

1. A narrow miss (one or two cases short) gets one unchanged rerun before anything is read or changed. Log it as a
   rerun and quote both runs. Never rerun again to get a better number.
2. A run cut short by credit or an outage does not count. Rerun it as it was.
3. A second miss stops the work. Bring the owner the totals and the options.
4. Reading a held-out miss needs the owner's word each time. Then fix only what it shows, move that case into
   tuning, and replace it with a new judged case.
5. A case or a label changes after a miss only when it contradicts the agreed design. Log the change beside the
   failing run. Anything else about a case, a label or a mark goes to the owner.

## Trap cases

- For safety checks, plant traps by construction: text addressed to AI tools, hidden text, look-alike sources,
  false figures. The mark for sure cases is 100%.
- A trap's marker words must appear nowhere else in its case, or true words will be counted as a leak.

## After a fix

- If the fix changes what a model is sent, measure again on the changed path.
- If it does not, prove it: compare the full request for every case before and after. Identical requests mean the
  measured runs stand. Say which path the comparison covers.

## The record

- Write down every run: what it measured, its totals, its cost, and why it ran.
- The harness prints "no cases" for an empty set, never a percentage, and an empty set never counts as a mark met.
- Report a small sample as its count, such as "5 of 5", not as a strong percentage.
- A shipped miss stays on record with the mark unmoved, and the owed measurement is listed with its cost.
- The documents quote the numbers for the path that ships. The commit carries one bullet and the record's path.
