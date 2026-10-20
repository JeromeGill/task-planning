# Docs

Project documentation. Read the relevant pages before starting work, and update
them in the same change when you alter what they describe (see
[Maintaining these docs](#maintaining-these-docs)).

| Page                                  | Read it when…                                                                    |
| ------------------------------------- | -------------------------------------------------------------------------------- |
| [Architecture](architecture.md)       | you need the big picture                                                         |
| [Development guide](development.md)   | setting up, running the app, or doing a common task                              |
| [Testing](testing.md)                 | running or writing tests                                                         |
| [Stories](stories/README.md)          | starting a feature or fix, or asking what a feature is meant to do               |
| [Plans](plans/README.md)              | the work is bigger or less certain than one story (new platform, new test layer) |
| [Troubleshooting](troubleshooting.md) | something fails in a way you didn't expect                                       |

## Maintaining these docs

- Docs describe the code as it is. When a change makes a page wrong (renamed
  file, new script, different behaviour), fix the page in the same commit.
- When you choose something a future reader would otherwise question or
  undo, say why on the page about it, in its "Why it's built this way"
  section: the alternatives rejected and when to revisit. There's no
  separate decisions log; the reason lives next to what it explains.
- Add a [troubleshooting](troubleshooting.md) entry when you hit and solve a
  confusing failure.
- Keep pages about _how and why_; don't paste code that is easy to read in the
  source. Link to files instead.
