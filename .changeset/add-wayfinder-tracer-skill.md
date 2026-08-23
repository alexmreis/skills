---
"mattpocock-skills": patch
---

Add the `wayfinder-tracer` skill (engineering bucket, user-invoked). It wraps `wayfinder` for efforts whose destination is merged code rather than a spec, without forking it: the map format, ticket mechanics and frontier are read from the sibling skill unchanged, and only ticket types, charting breadth and the `## Notes` block are overridden. Charting is depth-first and capped at a single `wayfinder:tracer` ticket (the simplest end-to-end slice that could possibly work) with `Not yet specified` left empty, replacing the breadth-first frontier sweep. The standing rules go into the map's Notes as a doctrine, so later plain `wayfinder` sessions inherit them: a question earns a ticket only once a merged tracer has run into it, tracers block the questions they answer except where a wrong answer outlives the branch, and resolutions carry evidence rather than conclusions.
