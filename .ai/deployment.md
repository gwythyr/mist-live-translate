# Deployment

- Deploy = `git push origin master`. GitHub Pages (legacy build) serves the repo root of `master` at https://gwythyr.github.io/mist-live-translate/ with `https_enforced`. No CI, no build step — `index.html` is the whole app.
- HTTPS is mandatory, not cosmetic: `getUserMedia` and `AudioWorklet` are secure-context only.
