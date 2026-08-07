# Design constraints

- 2026-08-06: the owner rejected the first design as "дуже дрібний, слабочитабельний". Readability is the priority — this is a two-person, arm's-length, in-conversation app. Keep body ≥17px, secondary labels ≥13px, touch targets ≥44px; never reintroduce 10–12px UI text.
- The translation feed is the hero surface: it takes the flexible middle of the layout, controls live in a fixed bottom bar. Its text size is the `--fs` custom property, driven by the A− / A+ header control (steps `FS_STEPS = [17,20,24,28,33]`, persisted as `mist.fs`).
- Never print a language name in the ear-state line — the `<select>` right above already shows it.
- 2026-08-07: layout invariant that replaced the overlapping first build — every band (`header`, `#ears`, `#guide`, `#controls`) is `flex:none` so it can never be squeezed into its own content; `#feed` is the ONLY `flex:1 1 auto; min-height:0` element and absorbs all slack; `#settings` is `position:fixed` so opening it cannot move a pixel. Do not give a band `flex-shrink:1` — that is exactly what made the old UI overlap.
- Horizontal blowout rule: `#ears` uses `minmax(0,1fr)` columns (plain `1fr` is `minmax(auto,1fr)` and cannot go below a `<select>`'s min-content width) and `.ear` carries `min-width:0`. In the pair card the `<select>` is borderless with an accent underline, not a pill — the pill's padding cost ~45px and truncated "Українська" on a 390px phone.
- The pair card has two densities driven by `body.running`: idle = tag + select, live = select + `.earstate`. Both are exactly two rows, so starting a session causes no layout jump. Keep it that way.
- `#guide` sits directly above `#controls` (instruction next to the action it leads to), not under the pair card.
- 2026-08-07: візуальна мова — темне скло над живим полем світла (референси: dark glassmorphism + aurora/mesh gradients, audio-reactive voice UI). Не пласкі 1px рамки, а градієнтна волосинка через `::after` + `mask-composite: exclude`.
- `.aurora` прив'язана до колонки застосунку (`position:fixed; left:0;right:0;max-width:720px;margin-inline:auto`), а НЕ до вьюпорта: на десктопі vw-прив'язка розносить плями до країв екрана і лишає колонку в темряві.
- Тло сторінки живе на `html`, `body` прозорий. Інакше `.aurora` із `z-index:-1` малюється ЗА фоном body і зникає.
- Жодного `filter: blur()` в анімованому шляху — радіальні градієнти й так м'які, а блюр перерастеризується щокадру. Плями рухає лише `transform`.
- `#viz` (29 смуг, тільки `transform: scaleY`) замінив пласку смужку мікрофона: свіжий відлік входить у центрі й розходиться до обох вух. Спокій і ефір ділять один силует `arch`, тож при старті форма не стрибає. Він же живить `--energy` для `.aurora`.
- Порожня стрічка містить `#hero` — знак моста у повний зріст. Ховається через `#feed[data-has]`, який ставить `addMsg`. `#hero` назавжди лишається `#feed.children[0]`, тому обрізання за `feedCap` видаляє `children[1]`, а не `firstChild`.
- Візуалізатор коштує ~19px висоти стрічки на портретних телефонах проти старої смужки. Драбинка `@media (max-height: 700px / 560px)` повертає їх на низьких екранах — у альбомній орієнтації новий макет на ~7px просторіший за старий.
- `--glass` має непрозорий середній стоп: там, де `backdrop-filter` недоступний, поверхня все одно читається. Радіус блюру тримати малим — `#ears` висить над рухомою aurora і переблюрюється щокадру.
