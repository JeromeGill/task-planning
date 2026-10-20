# Stories

Every feature has a user story here: what it does for the user and how to tell
it's done. They replace an external tracker. Stories are versioned with the
code, reviewed in the same branches, and linked to commits by a trailer.

## Writing a story

1. Pick the next free number, one above the highest ever used on any
   branch (a number in use on another branch or an open PR isn't free):

   ```sh
   git fetch && git log --all --name-only --format= -- docs/stories \
     | grep -o 'stories/[0-9]\{4\}' | sort -u | tail -1
   ```

2. Copy [`_template.md`](_template.md) to `NNNN-short-slug.md`, and fill in
   the story and acceptance criteria. Set `status: proposed`.
3. Commit it on its own (`docs(stories): add S-NNNN <title>`) on a `docs/`
   branch and merge it to `main` in its own small PR, so the number is taken
   before work starts. The feature is then built on a branch named after the
   story: `feat/S-NNNN-short-slug`.

A story that changes the UI isn't done until its main flow has a browser
test, named after the criteria it covers.

Keep acceptance criteria to observable behaviour (what the user or an api
client sees), one per line and numbered, so tests and reviews can point at
them. Implementation details belong in the Implementation section, filled in
when the story is done.

Statuses are `proposed`, `in-progress`, `done`, and `dropped`, in each
story's front matter (there's no index table, so stories don't conflict
with each other); `grep -l "status: proposed" docs/stories/*.md` lists
them. Update the status as the work moves. A dropped story stays
in the folder so its number isn't reused.

Stories describe current behaviour, so keep them in step with the code. When
a change touches a story, update its acceptance criteria (and its text or
title if the change goes further) on the same branch. Add, reword, or remove
criteria without renumbering the others, since tests and commits cite them. A
larger change can instead be a new story that refers to the old one.

## Linking code to stories

- **Commits:** every `feat` and `fix` commit carries a `Story:` trailer, one
  line per story it touches:

  ```text
  feat(web): show mileage in the cars table

  Story: S-0005
  ```

  commitlint enforces this (`commitlint.config.mjs`): it rejects a `feat` or
  `fix` commit without the trailer, or one naming a story that has no file
  here. Other types (`docs`, `refactor`, `build`, …) don't need it. Find a
  story's commits with `git log --grep "Story: S-0005"`.

- **Tests:** start the names of tests written for a criterion with the story
  and criterion IDs, e.g. `it("S-0005 AC2: rejects a reading lower than an
  earlier one")`, so `vitest run -t S-0005` (or, for browser tests,
  `playwright test -g S-0005`) runs a story's tests.

- **Code comments:** don't reference stories in code. The commit history
  links them, and comments that point to stories go stale.
