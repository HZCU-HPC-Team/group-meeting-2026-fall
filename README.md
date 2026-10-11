# group-meeting-2026-fall

Group meeting materials for **HZCU HPC Team**, Fall 2026.

This repository covers one semester. Next semester gets its own repository
(`group-meeting-2027-spring`), so nothing here needs renaming or migrating.

## Structure

```
group-meeting-2026-fall/
├── instructor/                # Organized by week
│   ├── W01/
│   │   ├── this-week.md           # What this meeting covered
│   │   └── next-week-tasks.md     # What to finish before next time
│   └── W02/
├── student/                   # Organized by deliverable
│   └── assignments/
│       ├── README.md              # Assignment list and status
│       └── topic-a-yourname/
└── README.md
```

## Two tracks

**Instructor track** — organized by week. Answers: *what did we discuss, what needs doing next*.
One `Wxx` folder per meeting. Existing weeks are append-only; don't rewrite past entries,
add to them.

**Student track** — organized by assignment. Answers: *who owes what, has it been turned in*.
One folder per topic + name. Status is summarized in `student/assignments/README.md`.

The two tracks do not overlap: instructors do not edit student folders, and students do not edit
instructor folders. Changes are traced through commit messages.

## Week numbering

`W01`, `W02`, ... starts at 1, zero-padded to two digits, matching the meeting index of the semester.
Create a new folder when a meeting happens — don't batch several weeks into one commit.

## Adding a new week

```bash
mkdir -p instructor/W02
git mv instructor/W01/this-week.md      instructor/W02/this-week.md
git mv instructor/W01/next-week-tasks.md instructor/W02/next-week-tasks.md
git commit -m "Add W02"
```

Keeping the two files per week makes diffs readable and shows what changed since last meeting.

## Commit conventions

- One logical change per commit; state which week and what changed
- Check file size before committing — keep individual files under 50 MB
- For large assets or files needing version retention, use GitHub Releases instead of this repository