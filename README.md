# pgSentinel 🛡️
> Enterprise PostgreSQL Health Monitor, Automated WAL Archiving & Point-In-Time Recovery (PITR) Engine.

![PostgreSQL Version](https://img.shields.io/badge/PostgreSQL-14%2B-blue)
![Platform](https://img.shields.io/badge/Platform-Ubuntu%20Linux-orange)
![License](https://img.shields.io/badge/License-MIT-green)

pgSentinel automates zero-downtime physical base backups, maintains continuous Write-Ahead Log (WAL) archiving, and provides deterministic disaster recovery down to the exact second using native PostgreSQL streaming replication primitives.

## 🚀 Key Architecture Features
* **Zero Transaction-Loss RPO:** Continuous WAL archiving (`wal_level = replica`) captures live database deltas to an isolated persistent mount.
* **Point-In-Time Recovery (PITR):** Replays WAL segments up to target timestamps to safely revert schema drops, ransomware events, or accidental table truncations.
* **Cryptographic Verification:** Every base backup archive is generated via `pg_basebackup`, compressed with `gzip`, and verified with SHA-256 integrity seals.
* **Principle of Least Privilege (RBAC):** Restricts automated backup workers to minimal `REPLICATION` and `SELECT` attributes.

## 🛠️ CLI Usage
```bash
# Check live cluster health and archiver queue
pgsentinel status

# Inspect active connections and disk consumption
pgsentinel health

# Create on-demand physical base backup with SHA-256 checksum
pgsentinel backup

# Trigger full disaster recovery up to a safe timestamp
pgsentinel pitr "2026-10-08 12:23:23"

