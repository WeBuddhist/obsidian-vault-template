# Plans — per-track convention

This folder holds calendar-driven study and practice arcs: daily readings, weekly retreat sessions, year-long courses, chanting schedules. Each plan organises engagement with the text along a calendar, generating per-session content from rails (and often from completed Translation or Adaptation outputs).

See [`../About Transformations.md`](../About%20Transformations.md) for the top-level rules that govern all transformation categories.

---

## Track structure

```
Plans/
└── [plan-id]/
    ├── requirements.md     # narrative brief governing the whole plan
    ├── termbase.md         # (optional) standard term renderings
    ├── audience.md         # audience profile
    ├── schedule/           # calendar.md, milestones.md
    ├── plans/              # the plan's internal arc structure (if multi-arc)
    ├── days/               # per-session content, one subfolder per language
    │   ├── [lang]/
    │   │   └── day-NNN.md
    │   └── _template/      # blank day template
    ├── communications/     # announcements, notifications, social-media posts
    │   ├── announcements/
    │   ├── notifications/
    │   └── social-media/
    └── assets/             # liturgy, audio, images
        ├── liturgy/
        ├── audio/
        └── images/
```

## Starting a new plan track

1. Create the folder `Plans/[plan-id]/`.
2. Author `requirements.md` covering: purpose, audience, per-session shape, languages published, source-rail dependencies, communications convention, status rules, and a sample session.
3. Scaffold `audience.md` from [`../../4-SYSTEM/Templates/audience.md`](../../4-SYSTEM/Templates/audience.md).
4. Create `schedule/calendar.md` with the full session calendar.
5. Create the `days/_template/` day template for the plan's session format.
6. Generate sessions one batch at a time from `complete` rails; iterate through QA before publishing.

## Citation in plan session files

Plan sessions may cite completed outputs of other tracks (e.g. embedding a Translation track's output for a reading step). Record all sources in the session file's `context_packages:` frontmatter — both the `2-RAILS/` packages and any `3-TRANSFORMATIONS/` outputs used.
