---
name: writing-tests
description: How to name, structure and write tests so they record what the product promises and fail only for real reasons. Use when writing or changing a unit, integration or browser test, when a test fails or flakes, and when reviewing tests.
---

# Writing tests

A test is a promise the product makes, written down. It reads as that promise and fails only when the promise is
broken. The project's own file names its framework, commands, fixtures, where each kind of test lives and its list
of known flakes; follow it, and use this for everything it leaves open. What a model writes is judged by evals
(the `eval-gates` skill), not by tests.

## Before writing

- Read the tests beside the code first. They say what is intended. Where a document and a test disagree, the code
  and its tests stand until the owner rules.
- Decide what a person can now do, or is now guaranteed, that they were not before. That sentence is the test.

## Names

- One grammatical sentence about what a person can do or is guaranteed, in the product's own words: "a member
  cannot book a class that is already full". Never a method name, a ticket or "works".
- The same for unit, integration and browser tests. A case drawn from a table or a list reads as a sentence too:
  check each one as it expands.

## What a test proves

- A fix starts with a test that fails for the reason being fixed. Watch it fail before making it pass.
- Assert outcomes: what a person sees, what is kept, what was sent. Not that a method was called, and never only
  that something exists.
- One promise a test. When behaviour changes on purpose, its test changes in the same commit, and the commit says
  why.
- A guard (a convention test, a lint rule) is shown to fail on a planted breach before it is trusted.

## Browser tests

- Wait for what the person sees: the waiting state, then the finished one. No sleeps. A wait with a number belongs
  only in a test about a time limit.
- Find things as a person does: by role, label and the words on screen. Never a test id or a styling class. Every
  control therefore needs an accessible name; a control that cannot be found this way is the defect.
- Cover each state the change adds, in each theme and screen size the project supports, and by keyboard.

## Data and isolation

- A test makes what it needs through the project's fixtures or factories, in the test database only, and cleans up
  after itself. Fixtures refuse to write anywhere else.
- A test leans on nothing an earlier test left. Where a suite runs in a fixed order on purpose, state left for a
  later test carries a comment saying why.
- Nothing outside the product is called for real. A recording stub or proxy answers, and the test asserts what was
  sent, not how long it took.
- Time is given to the code under test, never read from the wall clock.

## Structure

- One home for each promise, at the lowest level that can show it. Shared behaviour is proved once, where it
  lives; what a setting or a customer changes is proved at that setting's own level.
- An entry point gets a test for each outcome it can answer with; the unit of work behind it gets its rules tested
  directly; one test shows them composed.
- Where a second implementation is likely, write the cases once as a contract and run them against each.
- Two things at once (two tabs, a worker and a request) are proved with real concurrent workers or connections,
  not by reasoning about the code.

## Running

- Targeted tests while building. One heavy suite at a time on a machine: parallel suites produce false timeouts.
- Run what the change affects as you go, and the full run once on the final code (the `slice-delivery` skill,
  "Build and verify").

## Flakes

- A failure is real until proven otherwise. Rerun the file alone before calling it a flake, and name it either way.
- Known flakes live on one named list with their cause. Only those may be rerun without a finding.
- Never raise a timeout or add a sleep to hide one. A flake met twice is fixed, or listed with its cause.

## Reviewing tests

Read each new or changed test and ask:

- Does its name read as a promise a person would recognise?
- Take the fix away in your head: does the test fail, and for that reason?
- Does it assert an outcome, or only that something ran or exists?
- Any sleep, test id, styling class, wall clock or real outside call?
- Does it lean on another test's leftovers, or leave its own?
- Which promise in the change has no test at all?
