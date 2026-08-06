# Gotchas

- Local preview: the Chrome extension refuses `file://`. Serve with `python3 -m http.server <port>` from the repo root and open `http://localhost:<port>/index.html`.
- `resize_window` from the Chrome extension does not change `window.innerWidth` — responsive breakpoints cannot be verified that way; reason about them or use real devices.
