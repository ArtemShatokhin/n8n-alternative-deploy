# Deploy an open source n8n alternative with Docker Compose

Kortix self-hosts as one Docker Compose project. The frontend, the API, the LLM gateway and the Supabase distribution run on the box you choose, and agent sessions run on a separate sandbox provider. This is the deploy path for a team that wants the whole platform on its own infrastructure instead of a workflow engine on a server.

## What runs where

- **The control plane** is one Docker Compose stack on your host. It holds project state and serves the API.
- **Agent sessions** run off the box, on a sandbox provider. Each session gets its own isolated machine and its own branch, so thousands can run in parallel without touching each other.
- **The configuration** is a git repo you own: `kortix.yaml` declares the agents, what each may touch, and the triggers; behavior lives in markdown files under `agents/` and `skills/`; memory accumulates under `memory/`.

## Install

On a bare Linux box, the one-shot bootstrap installs Docker, installs the CLI, and starts the stack. Create the A/AAAA records for your domain and for `api.<domain>` first, and open ports 80 and 443.

```bash
curl -fsSL https://kortix.com/install | bash
kortix self-host init --domain kortix.example.com
kortix self-host start
```

On macOS, or on any host you would rather configure by hand, install the CLI and use the manual path:

```bash
kortix self-host init
kortix self-host start
kortix self-host doctor
```

## Evaluate without a domain

To try the stack before you own a domain, start it behind a Cloudflare tunnel:

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart, so run production on a real domain.

## What it needs, and what it does not

A self-hosted instance needs outbound network access; it is not an offline install. It pulls images from `docker.io/kortix/*`, and sessions never run on the box. The one credential the stack cannot start without is the sandbox provider key, set with `kortix self-host configure`; Platinum is the default, with Daytona available as a legacy fallback. There is no Redis and no separate worker. Each API service defaults to a 640 MiB memory limit, which suits an 8 GiB host; raise it on a 16 GiB host with `kortix self-host env set KORTIX_API_MEMORY_LIMIT=1024m`.

## Backups and updates

Copy two directories and one file under `~/.config/kortix/self-host/<instance>/`: the Postgres directory `volumes/db/data`, the storage directory `volumes/storage`, and the instance `.env`. A restore needs all three. Instances update themselves once a day by default; pin a version with `kortix self-host update --tag <version> --auto-update off` and roll back with `kortix self-host rollback --release <version>`.

The full reference is in the [Kortix docs](https://kortix.com/docs).
