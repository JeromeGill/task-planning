# task-planning

A lightweight, in-repo way to plan and track work: **stories** for features,
**plans** for bigger or uncertain work, and **GitHub issues** for small
follow-ups. Everything is Markdown versioned with the code, so it's reviewed
in the same PRs and stays in step with what was built.

## What's here

| Path                                                     | What it is                                                                           |
| -------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| [`docs/README.md`](docs/README.md)                       | Docs index skeleton and the rules for keeping docs current                           |
| [`docs/stories/README.md`](docs/stories/README.md)       | How stories work: numbering, statuses, linking commits and tests to criteria         |
| [`docs/stories/_template.md`](docs/stories/_template.md) | Story template                                                                       |
| [`docs/plans/README.md`](docs/plans/README.md)           | How plans work: when to write one, statuses, deleting them once implemented          |
| [`docs/plans/_template.md`](docs/plans/_template.md)     | Plan template                                                                        |
| [`commitlint.config.mjs`](commitlint.config.mjs)         | Conventional Commits plus a rule requiring a `Story: S-NNNN` trailer on `feat`/`fix` |
| [`CLAUDE.snippet.md`](CLAUDE.snippet.md)                 | Sections to paste into a project's `CLAUDE.md` / `AGENTS.md`                         |

## Using it in a project

1. Copy `docs/` into the project. Trim the `docs/README.md` table to the
   pages the project has.
2. Paste `CLAUDE.snippet.md` into the project's `CLAUDE.md` (or
   `AGENTS.md`).
3. Optionally enforce story trailers:

   ```sh
   pnpm add -D @commitlint/cli @commitlint/config-conventional
   ```

   copy `commitlint.config.mjs` to the repo root, and run
   `commitlint --edit "$1"` from a `commit-msg` hook (e.g. lefthook or
   husky).

4. Replace the example names (`S-0005`, `vitest`, `playwright`) in
   `docs/stories/README.md` with the project's own test runners.

## The workflow in short

- **Story first.** A feature starts as `docs/stories/NNNN-slug.md`
  (`status: proposed`) merged to `main` in its own small `docs` PR, so the
  number is taken. It's built on `feat/S-NNNN-slug`, and every `feat`/`fix`
  commit carries `Story: S-NNNN`. Tests are named `S-NNNN ACn: …`.
- **Plan when it's big or uncertain.** `docs/plans/NNNN-slug.md` records goal,
  options, proposal, open questions, the stories it produces, and its PRs.
  Once implemented, its lasting content moves to the docs and stories, and
  the plan is deleted.
- **No index tables**, so parallel PRs don't conflict; statuses live in front
  matter and `grep` lists them.
- **Reasons live next to what they explain**, in each docs page's "Why it's
  built this way" section, not in a separate decisions log.
