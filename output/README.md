# duckdb

> Fork of [dariogriffo/duckdb-debian](https://github.com/dariogriffo/duckdb-debian) (MIT); the original packaging is by Dario Griffo. Served at [deb.gaofn.xyz](https://deb.gaofn.xyz) for Debian 12 (bookworm) and 13 (trixie).

DuckDB is a fast, in-process analytical SQL database — think "SQLite for
analytics". This package ships the official `duckdb` CLI: run `duckdb` for an
interactive shell, or `duckdb mydb.duckdb` to work with a database file.
Extensions (httpfs, parquet, spatial, …) install at runtime from the official
extension repository, e.g. `INSTALL httpfs;`.

DuckDB is an embedded database: it runs inside the calling process, so there
is no server to configure and no systemd service — nothing to start or stop.

- Upstream: https://github.com/duckdb/duckdb
- Documentation: https://duckdb.org/docs/
- Packaging: https://github.com/gaofengnan/duckdb-debian
- Repository: https://deb.gaofn.xyz
