# dkg-infra

This repo holds environment and orchestration config only — Docker Compose
environments, CI/CD templates, monitoring, and secrets config. No
application source code lives here; that belongs in `dkg-platform`.

## Bringing up an environment

Each environment (dev, staging, prod) has its own env file and is brought up
as a separately named Compose project so multiple environments can run
concurrently on one VM.

Copy the example env file and fill in real values before starting:

```
cp .env.dev.example .env.dev
```

Then bring up the dev environment:

```
docker compose -p dev --env-file .env.dev up -d
```

Staging works the same way, with `.env.staging` and `-p staging`.

## Environments

- **dev** — available now.
- **staging** — available now.
- **prod** — the Compose configuration will support a prod environment, but
  it is intentionally not started yet.
