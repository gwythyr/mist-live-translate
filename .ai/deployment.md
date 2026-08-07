# Deployment

- The repo pins its own key in local config: `core.sshCommand = ssh -i ~/.ssh/gwythyr -o IdentitiesOnly=yes`. Without it the default key authenticates as `viktorshymko-devlight`, which is denied on this `gwythyr`-owned repo. `origin` stays the canonical `git@github.com:gwythyr/mist-live-translate.git` — no host alias, so a fresh clone only needs that one `git config` line.
- Deploy = `git push origin master`. GitHub Pages (legacy build) serves the repo root of `master` at https://gwythyr.github.io/mist-live-translate/ with `https_enforced`. No CI, no build step — `index.html` is the whole app.
- HTTPS is mandatory, not cosmetic: `getUserMedia` and `AudioWorklet` are secure-context only.
