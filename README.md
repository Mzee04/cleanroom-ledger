# Clean Room verdict ledger

This private repo is the verdict ledger for **Clean Room**, a submission integrity agent for data-science competitions.

Each Clean Room session opens one issue per candidate submission. The issue holds:

- the verdict (PASS / WARN / FAIL, and RECOMMENDED for the pick)
- the Sprite checkpoint the run was taken from
- the SHA-256 of the produced submission file
- whether the run reproduced from that checkpoint
- the competition-rule clauses involved, quoted word for word
- the trace lines behind each finding

Issues are posted by the agent Sprite through a Sprites GitHub connector. The Sprite never holds a GitHub token: the Sprites gateway attaches it, and the connector's access policy only admits Sprites named `cleanroom-agent*` and only paths under this repo.

A verdict says "no forbidden access detected" for what was traced in that environment. It is not a guarantee about anything outside the traced run.
