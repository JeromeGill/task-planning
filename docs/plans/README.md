# Plans

A plan is for work too big or too uncertain for a single story: a new
platform, a cross-cutting change to how the project is built or tested, or a
feature that needs design choices made before stories can be written. It
records the goal, the options, what was decided and why, and which stories
come out of it.

Smaller follow-ups, too small for a plan or a story, are
GitHub issues, closed from
the PR that does the work with `Fixes #N`.

Stories say _what_ the user gets and how to tell it's done. Plans say _how we
get there_ when that isn't obvious. Many features need no plan at all.

Plans have no index table, so plan PRs don't conflict with each other.
Open plans are the files in this folder; `grep -H "^status:"
docs/plans/0*.md` lists them with their status. Implemented plans are
deleted, and git history keeps them.

## Writing a plan

1. Pick the next free number, one above the highest ever used on any
   branch, deleted plans included:

   ```sh
   git fetch && git log --all --name-only --format= -- docs/plans \
     | grep -o 'plans/[0-9]\{4\}' | sort -u | tail -1
   ```

2. Copy [`_template.md`](_template.md) to `NNNN-short-slug.md` and set
   `status: draft`.
3. Commit it on a `docs/` branch (`docs(plans): add P-NNNN <title>`) and
   merge it to `main` in its own small PR before any work starts, so the
   number is taken; that's also the point of writing it down.

Statuses:

- `draft`: written down, not yet discussed or agreed.
- `investigating`: needs spikes or research before a choice can be made.
- `accepted`: the approach is agreed; its stories can be written.
- `done`: every PR in its PRs section is merged. The plan's file is then
  deleted (see below).
- `dropped`: decided against. The file stays as the record of why.

Update the status in the plan as it moves. When a plan is accepted, write
its stories (see [Stories](../stories/README.md)) and list them in the
plan's Stories section.

**Implemented plans are deleted**, usually in the PR that finishes the
work. Before deleting one, move what's still worth knowing out of it: how
things work to the docs pages, the reasons a future reader might otherwise
undo (rejected alternatives, "revisit when…") to the page's "Why it's built
this way" section, and what was built to its stories' Implementation
sections. Then fix every link to it; mention the plan by ID without a link.
