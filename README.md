# How I work

How I work with coding agents, as one always-on agreement and four skills. Portable: nothing in it names a project.

- `AGENTS.md`: the always-on agreement, read into every session. Short on purpose.
- `skills/adversarial-review/SKILL.md`: the reviewer's rules, brief, report and fix rounds, and the drift review.
- `skills/slice-delivery/SKILL.md`: the loop from brief to production, and running several builders.
- `skills/eval-gates/SKILL.md`: evals with fixed pass marks, held-out and fresh sets, misses, caps.
- `skills/writing-tests/SKILL.md`: how tests are named, structured and written, and how flakes are handled.

## To use it everywhere

    cp AGENTS.md ~/.claude/working-agreement.md
    mkdir -p ~/.claude/skills
    cp -R skills/adversarial-review skills/slice-delivery skills/eval-gates skills/writing-tests ~/.claude/skills/

Then add one line to `~/.claude/CLAUDE.md`: `@~/.claude/working-agreement.md`. Run `/memory` in a new session to
check that it loaded. Do not copy `AGENTS.md` into a project's root: the project's own standards file has that name.
The agreement carries my writing and commit rules too; if `~/.claude/CLAUDE.md` already states them, keep them in
one place.

A project still needs its own file for what is specific to it: the stack, the fixed places for each kind of file,
the design system, the commands that must pass, its test tools, fixtures and list of known flakes, where records
live, any standing word to commit, push or deploy, and its rulings. It states only what is specific or different,
never what the agreement already says. This folder is the source: after an edit here, copy again.

## License

MIT. See `LICENSE`.
