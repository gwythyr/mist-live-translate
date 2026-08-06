# Design constraints

- 2026-08-06: the owner rejected the first design as "дуже дрібний, слабочитабельний". Readability is the priority — this is a two-person, arm's-length, in-conversation app. Keep body ≥17px, secondary labels ≥13px, touch targets ≥44px; never reintroduce 10–12px UI text.
- The translation feed is the hero surface: it takes the flexible middle of the layout, controls live in a fixed bottom bar. Its text size is the `--fs` custom property, driven by the A− / A+ header control (steps `FS_STEPS = [17,20,24,28,33]`, persisted as `mist.fs`).
- Never print a language name in the ear-state line — the `<select>` right above already shows it.
