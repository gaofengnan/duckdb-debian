# duckdb-debian

> Fork of [dariogriffo/duckdb-debian](https://github.com/dariogriffo/duckdb-debian) (MIT); the original packaging is by Dario Griffo. Served at [deb.gaofn.xyz](https://deb.gaofn.xyz) for Debian 12 (bookworm) and 13 (trixie).

Debian and Ubuntu packaging for [DuckDB](https://duckdb.org) — a fast,
in-process analytical SQL database ("SQLite for analytics"). It reads and
writes CSV, Parquet and JSON directly, speaks rich SQL with excellent
performance on analytical workloads, and installs extensions (httpfs,
spatial, …) at runtime from the official extension repository.

The package ships the official `duckdb` CLI, built from upstream's glibc
release binaries so runtime extension installs (`INSTALL httpfs;`) match the
official `linux_amd64`/`linux_arm64` extension platforms.

DuckDB is an embedded database: it runs inside the calling process, so there
is no server daemon, no configuration and no systemd unit — install it and
run `duckdb`.

Packages are built automatically from official upstream releases (usually
within hours) and served from **[deb.gaofn.xyz](https://deb.gaofn.xyz)** for
Debian (bookworm, trixie, forky, sid) and Ubuntu (jammy, noble, questing,
resolute) on amd64 and arm64 (the architectures upstream publishes Linux
CLI binaries for).

## Install

```bash
sudo install -d -m 0755 /etc/apt/keyrings
sudo curl -fsSL https://deb.gaofn.xyz/deb.gaofn.xyz.gpg -o /etc/apt/keyrings/deb.gaofn.xyz.gpg
sudo curl -fsSL https://deb.gaofn.xyz/deb.gaofn.xyz.sources -o /etc/apt/sources.list.d/deb.gaofn.xyz.sources
# Debian 12 (bookworm): fetch deb.gaofn.xyz-bookworm.sources instead
sudo apt update
sudo apt install -y duckdb
```

Then:

```bash
duckdb              # in-memory interactive shell
duckdb mydb.duckdb  # persistent database file
```

### Manual Installation

1. Download the .deb package for your Debian version available on
   the [Releases](https://github.com/gaofengnan/duckdb-debian/releases) page.
2. Install the downloaded .deb package.

```sh
sudo dpkg -i <filename>.deb
```

## How it works

- `check-upstream.yml` polls upstream hourly; a new release dispatches `release.yml`.
- `release.yml` builds binary packages (Docker, per suite × architecture, from
  the upstream release binaries) and source packages (`.dsc`), then publishes
  a GitHub release tagged `<version>+<build>`.
- The deb.gaofn.xyz mirror ingests published releases automatically.

Manual build: `./build.sh <version> <build> [arch|all]` (e.g. `./build.sh 1.5.4 1 all`).

## Links

- Upstream: https://github.com/duckdb/duckdb
- Repository: https://deb.gaofn.xyz
