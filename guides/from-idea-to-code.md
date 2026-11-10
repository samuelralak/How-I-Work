# From a requirements document and a prototype to code

Nothing is built from memory or from a conversation. Each stage leaves a file, the next stage is built from that
file, and the owner's rulings go back into it the day they are made.

## The order

1. **Research.** Before specifying, study the closest existing work and the evidence for the problem. One short
   report per question, with its sources, in a research folder. Say what is borrowed and what is left out.
2. **The requirements document.** One file. See its shape below.
3. **The prototype.** Settles what a person sees and does, before any real code. See below.
4. **Freeze, then a design system.** When the owner says the design is settled, the prototype is frozen as a
   reference and its look is extracted into one design system: tokens, components, patterns, copy rules. From then
   on the design system is the visual truth, not the prototype.
5. **Technical research and spikes.** For each risky dependency or unknown, a small throwaway test with real data
   and a written result. A spike's code never becomes the product's.
6. **Design before code.** One document that walks every process step by step and names the decisions it rests
   on. No code yet.
7. **A contradiction pass.** While designing, check the requirements document against itself and against later
   rulings. List every contradiction and every missing decision, each with a proposal; the owner resolves them in
   one sitting, and the document takes a new version.
8. **Foundations.** The standards file, the base classes, the approved dependencies, the design system in the app.
   A few commits, before any feature.
9. **Screens first, on made-up data.** Build the screens from the prototype and the design system, with invented
   data behind services that already have their real names and return their real shapes.
10. **A build plan.** Ordered milestones that replace the made-up data one service at a time without changing a
    screen or its tests.
11. **Journey by journey.** One user journey to the end before the next. Each new mechanism gets a short design
    note; each slice is reviewed; anything a model writes is gated by evals.

Skip a stage only by saying so and why. A small product still writes the requirements, shows the screens before
building them, and lists its decisions.

## The requirements document

- **Why, who and what first:** the problem with its evidence, goals and non-goals, the people it is for, the
  principles that are not up for trade, the scope, and the main journeys told as a person lives them.
- **Requirements a builder can test:** each has a stable id by area, one sentence a test could check, and a
  priority (must, should, later, not planned). An id is never reused; a changed requirement is edited in place.
- **The system:** how anything a model writes is bounded and checked, the data model, the architecture, the
  experience (what each screen holds, in a table).
- **The business:** costs with their assumptions, metrics, trust and legal, release plan, risks, the alternatives
  that were rejected and why.
- **Decisions:** two lists kept apart. Decided, each numbered, dated and in the owner's words where they matter.
  Still open, each with a recommendation.
- **A changelog:** version, date, what changed and which requirements it touched.

A ruling said in conversation is not real until it is in this document. The day the owner rules, the requirement
is edited, the decision is numbered, and the changelog says so. Where the owner's picture and the document differ,
say so at once: one of them is about to be built.

## The prototype

- One self-contained file a person can open, covering every screen and state with one invented person's data. No
  backend, no real accounts, no real data.
- It answers questions about the experience: what is the home, what moves where, what each state says. Each round
  with the owner changes the prototype and the experience section of the requirements together.
- Build new versions beside the current one and replace it only when its checks pass, so the owner never opens a
  half-built screen.
- When it is frozen, keep the frozen version untouched. Later, once real screens exist, they are the newest
  design: a new prototype follows them and the design system, never the other way round.

## Building from a prototype

- Before any screen work, read the prototype's part for that screen and render it. Say what it specifies, then
  the plan, with every departure listed apart and its reason.
- Build the real screen with the design system's tokens and components, not by copying the prototype's markup.
- What the prototype does not show (an empty, refused, waiting or failed state, a phone, a keyboard) is designed
  in the same language and shown to the owner, not improvised in code.
- When the owner asks for a change to a built screen, change that element. A new direction goes back through the
  prototype first.

## Keeping it true

- Later rulings override earlier ones; the documents say which is which by date and decision number.
- A design note that changes what the requirements say updates the requirements in the same piece of work.
- Before building a feature, read its requirements, its design note and its prototype screens again, and say
  aloud the rule you are about to build. If the owner's words differ from the file, stop and settle it.
