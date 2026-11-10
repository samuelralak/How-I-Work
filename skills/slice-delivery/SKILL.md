---
name: slice-delivery
description: Deliver a change to code as a small reviewed slice, from brief to production. Use when building or fixing code that will be committed, when briefing a builder agent or checking its handover, when several builders share a codebase, and before a commit, push or deploy. Not for a change to docs or code comments alone.
---

# Slice delivery

The loop for a slice: brief, build, verify, review, commit, deploy, with records kept as the working agreement says.
Working alone, you are the builder: skip step 1 and "Several builders at once". With no deploy, skip step 5.

## 1. Brief the builder

A builder has the working agreement and what the brief says. Give it:

- the goal and why it matters now;
- the files and documents to read first, including the standards file;
- the rules that apply and the rulings already made;
- what is out of bounds: other builders' paths, shared files, uncommitted work that is not its own;
- where to build and which test database to use;
- what comes to you first: a paid call, a change to an agreed design, a product question;
- to load this skill and follow "Build and verify", and the `writing-tests` skill for every test it writes.

The handover wanted: the path list, the diff or a patch against the head, which tests failed first, each check it
ran with its totals, the head it ran on and when any bundle was built, what it found, what changes for a person,
any step needed after deploy, and what it did not do.

## 2. Build and verify

- A design note first for a new mechanism. Tests by the `writing-tests` skill: a failing test first for a fix,
  named as a promise, asserting outcomes. An organisation pass on your own diff before handing over: places, names,
  duplication, dead code.
- Run what the project's file says must pass, once, on the final code, with no other suite running. If it names
  nothing: the full suite, the browser tests, lint and static checks.
- Tests run against the code as it is now. After editing a script or a stylesheet, rebuild before a browser run. A
  run counts only if the build is newer than the last edit; report both times.
- A failure outside the slice is rerun alone and named either way. It is a flake only if it is on the project's
  list of known flakes, or goes onto it with its cause; anything else is a finding.

## 3. Review

First check a builder's handover yourself: the patch applies to the head, its paths match the list, and the totals
are from the final code. Then use the `adversarial-review` skill. Nothing is committed while a blocker stands.

## 4. Commit

- With the owner's word only, given then or standing in the project's file. The same goes for a push and a deploy.
  Without it, stop at "ready to commit" and say so.
- Check what is staged, then commit by path (`git commit -- <paths>`): a plain commit takes whatever anyone
  staged. Never amend or reset.
- The commit holds exactly what was reviewed: compare its paths and its diff with the reviewed change.
- The message follows the owner's commit rules. A known miss is one bullet naming its record; numbers stay there.

## 5. Deploy and check

- List the commits since the last deploy in a step of its own and read them. Deploy only if every one is reviewed.
- Check production with a read-only script: the version running, schema changes applied, new code loading, no failed
  work since the deploy. Report what it showed.
- A data step is a separate task, previewed read-only first, with its size told to the owner before it runs.

## Several builders at once

- Give each its own paths and test database. Name each shared file and the one builder who may change it; the
  others send it their lines. A commit of a shared file takes the head's version plus only that slice's lines.
- Builders never commit, stage, stash, reset or restore a whole file. They hand over a patch and you commit, in an
  order you decide. Tell each builder when the head moves so it rebases once.
- After each commit, check `git status` and the diff of every shared file against the head: the only differences
  are lines still in flight.
- A builder that must run tests while another is using the tree works in a scratch copy, removed when it is done.

## Reporting to the owner

- What is live, what is committed and not deployed, what is in review, what is built and waiting.
- For each: where it stands and what it needs next. Times are ranges, built from measured steps and the queue.
