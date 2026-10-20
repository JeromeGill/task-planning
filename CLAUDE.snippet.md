## Documentation

`docs/` holds the project documentation; `docs/README.md` is the index.

- **Before starting work, read `docs/README.md` and the pages relevant to the task.**
- **Every feature has a story** in `docs/stories/` (see `docs/stories/README.md`): story, numbered acceptance criteria, status in its front matter. A new feature starts with its story (`status: proposed`) landing on `main` in its own small `docs` PR, so its number is taken before work starts (`docs/stories/README.md` has the command that finds the next number); mark it `done` and fill in its Implementation section when the feature is finished. **A story that changes the UI isn't done until its main flow has a browser test**, named `S-NNNN ACn: …`.
- **Bigger or uncertain work has a plan** in `docs/plans/` (see `docs/plans/README.md`): goal, options, proposal, open questions, and the stories it produces. Plans land on `main` in their own `docs` PR before work starts; their stories are written once a plan is `accepted`. **Once a plan's work is merged, delete the plan**: first move its lasting content to the docs pages (reasons into their "Why it's built this way" sections) and its stories, and fix links to it.
- **Follow-ups are GitHub issues**: small cleanups or ideas that come up mid-task and aren't worth a plan or story yet go in `gh issue create --label <label>` (`bug`, `enhancement`, `chore`, `tests`, `infra`, `documentation`). Close them from the PR that does the work with `Fixes #N`.
- **Keep stories current.** When a requested change relates to an existing story, update that story in the same branch: adjust the acceptance criteria (add, reword, or remove; don't renumber the others, since tests and commits cite them), and the story text, notes, or title if the change goes further. **Before changing a story, show the user the proposed story changes and wait for confirmation**; don't edit a story's intent or criteria silently. If a change fits no story, propose a new one.
- **Keep the docs current.** When a change makes any page inaccurate (renamed file, new script, env var, behaviour change), update that page in the same commit. Record a non-obvious choice (rejected alternatives, when to revisit) in its page's "Why it's built this way" section, and a confusing failure you solve in `docs/troubleshooting.md`. If this file and `docs/` disagree, fix whichever is wrong.

## Branches and commits

- **Each task gets its own branch** from an up-to-date `main`, named `<type>/<short-description>` with a Conventional Commit type, e.g. `fix/table-mobile`; a story's branch starts with its ID, e.g. `feat/S-0006-service-reminders`.
- **Keep PRs small and scoped to one concern**, with their tests and docs. A story or plan that touches several functional areas can be several PRs, stacked when one depends on another.
- Use [Conventional Commits](https://www.conventionalcommits.org/) (enforced by commitlint): `<type>(<optional scope>): <description>`. `feat` and `fix` commits must end with a `Story: S-NNNN` trailer (one per story) naming a file in `docs/stories/`; a custom rule in `commitlint.config.mjs` rejects them otherwise.
