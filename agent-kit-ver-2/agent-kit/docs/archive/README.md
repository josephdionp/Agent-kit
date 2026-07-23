# Archive

Historical and superseded material. **The agent ignores this folder unless
explicitly asked.** Anything here is superseded by `project/`, `development/`,
`status/`, or `plans/`. Kept for provenance only; never authoritative.

## Rules

- Never link from a live doc into `archive/`.
- If archived content becomes needed again, extract it into the appropriate
  live folder and re-cite it — do not link into archive.
- On dedup: when two archived files are byte-identical, keep one and note the
  drop in `OMITTED-DUPLICATES.md`.

## Suggested layout when content grows

```text
archive/
├── README.md
├── OMITTED-DUPLICATES.md      # what was byte-identical to a current file
├── legacy/                    # earlier versions of current docs
├── superseded-layout/         # entire old folder structures
├── completed-plans/           # done plans awaiting promotion (see plans/)
└── assets/                    # outdated diagrams, kept as evidence
```
