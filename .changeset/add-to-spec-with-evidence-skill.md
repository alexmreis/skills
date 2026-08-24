---
"mattpocock-skills": patch
---

Add the `to-spec-with-evidence` skill (engineering bucket, user-invoked). It runs `to-spec` and adds one line to each entry under **Implementation Decisions** that something actually proved: what ran, what came back, what it ruled out. Decisions reached by argument are written exactly as `to-spec` writes them, and the visible difference between the two is the point, since it tells a later reader which decisions a slice has already settled and which are still the best available reasoning. It is the step a `wayfinder-tracer` map graduates a proven chunk through, and is worth reaching for on any thread carrying that evidence.
