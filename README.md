# ECE 6765 public leaderboard data

This repository holds the data of the [ECE 6765 public
leaderboard](https://cornell-ece6765.github.io/ece6765-mkdocs/ece6765-leaderboard/).
A staff script rewrites `leaderboard.json` once a day. Do not edit it by hand.

## `leaderboard.json`

```json
{
  "schema": 2,
  "updated_at": "2026-11-18T14:00:00Z",
  "teams": [
    {"team": "team-01", "name": "team-01", "score": 0,
     "traces": {"short-query-answerable": 0, "long-query-answerable": 0,
                "short-query-unanswerable": 0, "long-query-unanswerable": 0},
     "counted_updates": 0, "last_counted": null}
  ]
}
```

- `schema`: the format version, 2. Version 2 adds `traces`.
- `updated_at`: the time of the daily update, in ISO 8601 UTC.
- `teams`: one entry per group, in any order. The page sorts them by score.
  - `team`: the repository name, `team-01` to `team-15`.
  - `name`: the name that the page shows.
  - `score`: the overall leaderboard score of the latest valid update, the
    geometric mean of its four trace scores, or 0 when the group has none.
    Only this score decides which updates count.
  - `traces`: the score of the latest valid update on each public trace, by
    trace name, or 0 for every trace when the group has none. With these
    scores the page can rank the groups on each trace.
  - `counted_updates`: the number of updates that count toward the
    participation bonus.
  - `last_counted`: the date of the last counted update, as `YYYY-MM-DD`, or
    `null`.

The page reads this file from
`https://raw.githubusercontent.com/cornell-ece6765/ece6765-leaderboard/main/leaderboard.json`,
so a push to `main` reaches the page within a few minutes, without a
redeploy of the documentation site. The file holds scores only. Reports,
answers, and reference answers stay out of this repository.
