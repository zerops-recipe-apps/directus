# Agent notes — directus (Zerops recipe app)

- **Recipe imports** live in [zeropsio/recipes/directus](https://github.com/zeropsio/recipes/tree/main/directus), not in this repo.
- **Runtime:** `alpine/nodejs@24`, Directus **12.x** via npm (`directus start` on port **8055**). Probes use **`/server/ping`** (health endpoint is auth-only in v12).
- **Install:** root `.npmrc` sets `ignore-scripts=true`. Zerops build runs `npm install-scripts approve` + `npm rebuild` for `isolated-vm`, `argon2`, and `esbuild` after `npm ci`.
- **Override:** `isolated-vm@7.0.1` in `package.json` — required for Node 24 (Directus still pulls 5.x transitively otherwise).
- **Setups:** `development` (Mailpit SMTP, `SEED_VERSION`), `production` / `directus` (HA). Vault supplies `SECRET`, `ADMIN_TOKEN`, `ADMIN_PASSWORD`, `ADMIN_EMAIL`. Valkey: `REDIS_HOST` / `REDIS_PORT` / `REDIS_PASSWORD` ← `${cache_*}`.
- **Local / dev:** use the [directus](https://app.zerops.io/recipes/directus) recipe **Local** or **Remote (CDE)** environment — no Docker in this repo.
