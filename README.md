# group-meeting

Shared repository for group meetings, archived by semester.

## Structure

```
group-meeting/
├── instructor/                # Organized by week
│   └── 2026-fall/
│       ├── W01/
│       │   ├── this-week.md        # What this meeting covered
│       │   └── next-week-tasks.md  # What to finish before next time
│       └── W02/
├── student/                   # Organized by deliverable
│   └── 2026-fall/
│       └── assignments/
│           ├── README.md           # Assignment list and status
│           └── topic-a-yourname/
└── README.md
```

## Two tracks

**Instructor track** is organized by week. It answers: *what did we discuss, what needs doing next*.
One `Wxx` folder per meeting. Existing weeks are append-only — don't rewrite history, add to them.

**Student track** is organized by assignment. It answers: *who owes what, has it been turned in*.
One folder per topic + name. Final status gets reflected in `student/<semester>/assignments/README.md`.

The two tracks do not overlap: instructors do not edit student folders, and students do not edit
instructor folders. Changes are traced through commit messages.

## Week numbering

`W01`, `W02`, ... starts at 1, zero-padded to two digits, matching the meeting index within a semester.
Each new semester gets a fresh `<year>-<season>` folder under `instructor/`, counting restarts at `W01`.

## Commit conventions

- One logical change per commit; state which week and what changed
- Check file size before committing — keep individual files under 50 MB
- For large assets or files needing version retention, use GitHub Releases instead of the git repository