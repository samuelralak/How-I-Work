---
name: adversarial-review
description: Brief, carry out or act on an independent adversarial review. Use before committing a slice, to recheck a fix round, when you are briefed as the reviewer, and when the owner asks for a drift review of architecture, design or standards.
---

# Adversarial review

One independent reviewer checks a slice before it is committed. Its job is to find what is wrong, not to confirm
that the work is done. If you are the reviewer, "Rules" and "The report" are yours; the rest is for whoever briefs you.

## Rules

- The reviewer is a separate agent that did not build the slice. It never edits the code under review. If you cannot
  start one, write the brief to a file and ask the owner to open a fresh session with it.
- Give it the code and the claims, never your conclusion. Ask it to attack; do not ask it to approve.
- It reviews the exact change that will be committed: the diff of the slice's paths against the head, or the
  builder's patch when the commit is built apart from the tree.
- It may run single targeted tests, never the full suite, a paid call or anything against shared data. Two agents
  never run tests on one database at once: it uses the builder's only after the builder's runs have stopped, or
  else one of its own, dropped when it reports.
- A finding is a defect traced in the code, probed with a small test when it rests on what happens at run time.
  What it could not trace is listed apart as a question.
- Two passes: the review, then one recheck of what changed. After that only a blocker still standing earns another.

## The brief

Tell the reviewer to load this skill; the brief then carries only what is specific to the slice:

1. What the slice is, in two or three sentences, and where the diff and the builder's notes are.
2. The sources of truth: the standards file, the design documents, earlier reviews of the same area.
3. What the slice claims to do, as a list. These are claims to test.
4. What to look hardest at. Draw from this list:
   - correctness under retries, restarts, races and two tabs;
   - safety: outside text reaching a model, private data reaching a log or a broadcast, access to another person's
     records, output escaping;
   - money: who is charged, how often, and what bounds it;
   - data: schema-only changes, existing rows, anything needing a step after deploy;
   - what changes for live behaviour the moment it deploys;
   - tests, against the `writing-tests` skill: named as promises, failing for the reason fixed, asserting outcomes,
     no sleeps or styling selectors; and important behaviour with no test;
   - organisation: files in their fixed places, names, duplication, dead code, drift from the agreed design;
   - the standards file, rule by rule, on everything the slice touches.
5. Which test database it may use, and what never to run.

A small slice (a few files; no money, safety or data) needs items 1 and 3, the organisation check and a read of
its tests only. The last
review of a feature of several commits also reads the whole feature for drift.

## The report

- Findings, most severe first. For each: severity (blocker, should fix, minor), file and line, one sentence on the
  defect, and the concrete scenario that goes wrong.
- What was checked and found sound, briefly.
- One closing line: commit as is, commit after the blockers, or do not commit.
- No praise, and no summary of what the slice does.

## After the report

1. Save the report with the slice's other records.
2. Decide what must be fixed before the commit: every blocker, and every finding of the same kind as a blocker
   (safety, money, data loss, a wrong answer). Product choices go to the owner with a recommendation.
3. The builder reads the whole report, fixes in one pass, each fix with a test that fails first, and answers every
   finding in one line. You settle a disputed finding by reading the code.
4. The same reviewer rechecks what changed. Nothing is committed while a blocker stands; everything else goes on
   the written follow-up list, with file and line.
5. A reviewer can be wrong. Before a finding reaches the owner or changes a plan, open the code or the data it rests
   on yourself.

## Drift review

For a review of a whole codebase against its standards, when the owner asks for one:

- One read-only reviewer per area, for example backend and interface, on the committed code. The standards file is
  law; drift the convention tests do not catch is the most valuable to find.
- Ask for: a one-paragraph verdict, findings by severity with the rule quoted, systemic patterns with counts,
  documents that are out of date, and what was not covered. Harm to a person, money or data is kept apart from
  tidiness.
- Bring the owner a ranked summary and let them choose what to fix first. Fix in reviewed slices, each with a guard
  so the rule stays fixed.
