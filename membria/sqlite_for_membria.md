---
icon: package
label: SQLite for Membria
order: 92
---

---

# In-Memory and Hybrid SQLite Use in Membria

## Overview

For edge-based reasoning, caching, and agent memory in Membria, SQLite provides an ideal lightweight storage engine. It supports pure in-memory mode, hybrid (in-memory + persistent), and optimized configurations with JSON support. This enables low-latency, private, and portable knowledge management directly on user devices.

---

## 🧠 SQLite Modes for Membria

### 1. Pure In-Memory Mode

```sql
sqlite3 :memory:
```

- Fully memory-resident database
- Fastest access (no disk IO)
- Data lost on shutdown
- Ideal for runtime reasoning chains or ephemeral KV caches

---

### 2. Hybrid Mode (In-Memory + Persistent Backup)

Use an in-memory database and periodically back it up to disk:

```sql
ATTACH DATABASE 'backup.db' AS disk;
BACKUP TO disk;
```

- Combines speed of RAM with persistence
- Useful for agent sessions with autosave
- Easy recovery on reboot

---

### 3. In-Memory Tables Inside Persistent DB

Within a persistent DB file, use temporary tables for volatile data:

```sql
CREATE TEMP TABLE kv_cache (...);
```

- Cached data is in RAM only
- Cleared when session ends
- Great for session-based reasoning cache

---

### 4. Shared Memory Mode

SQLite supports shared cache between threads or agents:

```sql
sqlite3 file:memdb1?mode=memory&cache=shared
```

- Enables multi-agent reasoning or shared context across threads

---

## ⚙️ Performance Boosters

### WAL Mode (Write-Ahead Logging)

```sql
PRAGMA journal_mode=WAL;
```

- Speeds up concurrent reads/writes
- Efficient for background syncs

---

### JSON Support (Built-in)

```sql
SELECT json_extract(payload, '$.step');
```

- JSON1 extension enables flexible querying
- Store reasoning steps, KV entries, events as structured JSON

---

## ✅ Use Cases in Membria

| Component           | SQLite Mode       | Description                                      |
|---------------------|-------------------|--------------------------------------------------|
| `kv_cache`          | TEMP Table        | Volatile session-level reasoning cache           |
| `event_log`         | Hybrid            | Persistent timeline of agent actions and events  |
| `reasoning_path`    | In-Memory         | Fast access to active chains                     |
| `local_index`       | Persistent        | Topic/domain embedding search support            |

---

## 📘 Summary

SQLite enables blazing-fast and privacy-preserving reasoning memory on-device:
- No server dependency
- No setup required
- Easily portable across devices
- Integrates seamlessly with Membria’s caching and reasoning stack

> Combine this with JSON schemas and local event graphs for full DoD agent memory and autonomy.

