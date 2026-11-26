# Clean Room verdict ledger

This public repo is the verdict ledger for **[Clean Room](https://github.com/Mzee04/cleanroom)**, a
submission integrity agent for data-science competitions. Anyone can read these issues.

Each Clean Room session opens one issue per candidate submission (the title carries the session id).
Re-running a session updates its issues instead of opening duplicates. Each issue holds:

- the verdict (PASS / WARN / INCONCLUSIVE / FAIL, and RECOMMENDED for the pick)
- the session, run id and the Sprite checkpoint the run was taken from
- the SHA-256 of the produced submission file and whether it reproduced from that checkpoint
  ("reproduced in the recorded environment": same checkpoint, libraries and hardware)
- the tracer used, whether the candidate ran as a separate uid, and whether egress denial was verified
- an environment fingerprint (Python, numpy, scikit-learn, kernel, CPU)
- the competition-rule clauses involved, quoted word for word, and the trace lines behind each finding
  (raw command lines and home paths are redacted; candidate-controlled text is Markdown-escaped)
- a canonical JSON record, its SHA-256, and `previous_issue_sha256`, the hash of the record published
  before it

The records form a hash chain: editing one changes its hash, and the next record still commits to the
old value; GitHub also keeps each issue's edit history. That makes the ledger tamper-evident, not
tamper-proof: nothing is signed or externally timestamped.

Issues are posted by the agent Sprite through a Sprites GitHub connector. The Sprite never holds a
GitHub token: the Sprites gateway attaches it, and the connector's access policy only admits Sprites
named `cleanroom-agent*` and only paths under this repo.

A verdict says "no forbidden access detected" for what was traced in that environment. It is not a
guarantee about anything outside the traced run. Issues #1–#5 come from an earlier version and are
closed, each with a link to its replacement.
