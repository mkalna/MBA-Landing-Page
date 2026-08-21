# MBA Hub — how it's wired & how to update it

## The two kinds of data

**Shared data** — the assignment list, due dates, and social events everyone
sees — lives in **`data/data.json`**. The page reads it fresh every time it
loads, so when you edit that file and publish, the change reaches everyone on
their next visit.

**Personal data** — each person's check-offs and anything they add via the
"+ Add" buttons — is saved only in that person's browser, keyed by item ID.
Updating `data/data.json` never wipes it.

## To update a due date or add/remove an assignment or event

Edit **`data/data.json`**. It looks like this:

```json
{
  "updated": "2026-08-20",
  "source": "manual",
  "assignments": [
    {"id":"a1","cls":"analytics","title":"Data Literacy Homework I","date":"2026-09-21","time":"17:00","type":"deliverable","weight":"25% (Homework total)","notes":"Submit via Canvas.","done":false}
  ],
  "social": [
    {"id":"s1","title":"Commencement Rehearsal","date":"2026-08-19","time":"","endTime":"","location":"Robins School of Business","tags":["robins"],"notes":"..."}
  ]
}
```

Field notes:
- **`id`** — must be unique and stable. Don't reuse an ID or change an existing
  one (people's check-offs are tied to it). New item = new unique id.
- **`cls`** — one of: `economics`, `accounting`, `analytics`, `ethics`, `strategy`.
- **`date`** — `YYYY-MM-DD`. **`time`** — 24-hour `HH:MM` or `""` for none.
- **`type`** — `deliverable`, `paper`, `presentation`, `quiz`, `reading`,
  `discussion`, or `other`. (Reading/discussion/other show under the
  "Reading/Other" filter; the rest show under "Deliverables".)
- **`tags`** (social only) — any of `networking`, `social`, `robins`.
- Bump **`updated`** to today's date so the "· updated …" stamp reflects it.

Tip: paste the file into any JSON validator before publishing to catch a stray
comma. A broken JSON file falls back to the built-in snapshot.

## Hosting

Put `index.html` and the `data/` folder in the repo root and enable GitHub
Pages (Settings → Pages → deploy from `main`, root). Editing `data/data.json`
in GitHub and committing is all it takes to update the live site.

> The full data is also embedded inside `index.html` as an offline fallback
> (used only if the page is opened directly from disk, where browsers block the
> data file from loading). `data/data.json` is the real source of truth — edit
> that. The embedded copy can be left as-is.
