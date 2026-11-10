# How I work

How I work with coding agents. Portable: nothing in it names a project.

## What is here, and why each is the kind of file it is

- **`AGENTS.md`, the agreement.** Rules that hold in every session: how I work, design, review, tests, the
  interface, usage, delivery, safety. Always loaded, so it stays short.
- **Three skills,** each a procedure with a clear moment, long enough to load only then:
  - `skills/adversarial-review/SKILL.md`: briefing a reviewer, the report, the fix rounds, a drift review.
  - `skills/slice-delivery/SKILL.md`: the loop from brief to production, and running several builders.
  - `skills/eval-gates/SKILL.md`: evals with fixed pass marks, held-out and fresh sets, misses, caps.
- **One guide,** read on demand and never loaded by itself:
  - `guides/from-idea-to-code.md`: starting a product from research, a requirements document and a prototype.

A rule goes in the agreement. A procedure becomes a skill only if it has its own moment and is too long to carry
always. Background for a rare moment is a guide the agreement points to. Nothing is said twice.

## To use it everywhere

    mkdir -p ~/.claude/how-i-work ~/.claude/skills
    cp AGENTS.md ~/.claude/how-i-work/AGENTS.md
    cp -R guides ~/.claude/how-i-work/
    cp -R skills/adversarial-review skills/slice-delivery skills/eval-gates ~/.claude/skills/

Then add one line to `~/.claude/CLAUDE.md`: `@~/.claude/how-i-work/AGENTS.md`. Run `/memory` in a new session to
check that it loaded. Do not copy `AGENTS.md` into a project's root: the project's own standards file has that name.
The agreement carries my writing and commit rules too; if `~/.claude/CLAUDE.md` already states them, keep them in
one place.

A project still needs its own file for what is specific to it: the stack, the fixed places for each kind of file,
the design system, the commands that must pass, its test tools, fixtures and list of known flakes, where records
live, any standing word to commit, push or deploy, and its rulings. It states only what is specific or different,
never what the agreement already says. This folder is the source: after an edit here, copy again.

## License

MIT. See `LICENSE`.
