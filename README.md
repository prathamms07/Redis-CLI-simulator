# Redis CLI Simulator 🟥

> A fully functional Redis CLI simulator that runs entirely in your browser — no backend, no Docker, no server required.

**[Live Demo →](https://your-username.github.io/redis-cli-simulator)**

![Redis CLI Simulator](https://img.shields.io/badge/redis-7.2-red?logo=redis&logoColor=white)
![No Backend](https://img.shields.io/badge/backend-none-brightgreen)
![GitHub Pages Ready](https://img.shields.io/badge/deploy-GitHub%20Pages-blue?logo=github)

---

## Features

- **50+ Redis commands** — strings, lists, hashes, sets, sorted sets, key ops, server commands
- **Real Redis semantics** — TTL/EXPIRE with actual timers, WRONGTYPE errors, correct return types
- **Command history** — navigate with ↑ / ↓ arrow keys
- **Tab completion** — press Tab to autocomplete commands
- **Quick reference sidebar** — click any command to insert a template
- **Zero dependencies** — single `index.html`, no npm, no build step

---

## Supported Commands

| Category      | Commands |
|---------------|----------|
| **Strings**   | SET, GET, MSET, MGET, INCR, INCRBY, DECR, DECRBY, INCRBYFLOAT, APPEND, STRLEN, GETRANGE, SETRANGE, GETSET, GETDEL, SETNX, SETEX, PSETEX |
| **Keys**      | KEYS, EXISTS, DEL, UNLINK, TYPE, RENAME, COPY, EXPIRE, EXPIREAT, PEXPIRE, TTL, PTTL, PERSIST, RANDOMKEY, SCAN, DBSIZE, FLUSHDB, FLUSHALL |
| **Lists**     | LPUSH, RPUSH, LPUSHX, RPUSHX, LPOP, RPOP, LLEN, LRANGE, LINDEX, LSET, LREM, LINSERT, LTRIM, RPOPLPUSH |
| **Hashes**    | HSET, HGET, HMSET, HMGET, HDEL, HEXISTS, HLEN, HKEYS, HVALS, HGETALL, HSETNX, HINCRBY, HINCRBYFLOAT |
| **Sets**      | SADD, SREM, SMEMBERS, SCARD, SISMEMBER, SMISMEMBER, SUNION, SINTER, SDIFF, SUNIONSTORE, SINTERSTORE, SDIFFSTORE, SPOP, SRANDMEMBER, SMOVE |
| **Sorted Sets** | ZADD, ZSCORE, ZINCRBY, ZRANK, ZREVRANK, ZCARD, ZCOUNT, ZRANGE, ZREVRANGE, ZREM, ZPOPMIN, ZPOPMAX |
| **Server**    | PING, ECHO, SELECT, INFO, COMMAND, DBSIZE, DEBUG, RESET, QUIT |

---

## Deploy to GitHub Pages (2 minutes)

### Option A — Upload via GitHub UI

1. Create a new repository on GitHub (e.g. `redis-cli-simulator`)
2. Click **Add file → Upload files**
3. Upload `index.html`
4. Go to **Settings → Pages**
5. Set source to `main` branch, root `/`
6. Click **Save** — your URL appears in ~60 seconds

### Option B — Git CLI

```bash
git clone https://github.com/your-username/redis-cli-simulator
cd redis-cli-simulator
cp /path/to/index.html .
git add index.html
git commit -m "Initial commit"
git push origin main
```

Then enable GitHub Pages in **Settings → Pages → Source: main / root**.

### Option C — GitHub CLI

```bash
gh repo create redis-cli-simulator --public
cp index.html .
git add . && git commit -m "Initial" && git push
gh api repos/:owner/redis-cli-simulator/pages -X POST -f source='{"branch":"main","path":"/"}'
```

---

## Run Locally

No build needed:

```bash
# Python
python3 -m http.server 8080

# Node
npx serve .

# Or just open index.html directly in your browser
open index.html
```

---

## Usage

```
127.0.0.1:6379> SET user:1 "Alice"
"OK"

127.0.0.1:6379> HSET user:1:profile name Alice age 30 city Mumbai
(integer) 3

127.0.0.1:6379> HGETALL user:1:profile
1) "name"
2) "Alice"
3) "age"
4) "30"
5) "city"
6) "Mumbai"

127.0.0.1:6379> EXPIRE user:1 60
(integer) 1

127.0.0.1:6379> TTL user:1
(integer) 59
```

---

## Architecture

Everything runs in the browser — `index.html` contains:

- **In-memory store** — 16 Redis databases (`Map`, `Set`, `Array`, custom `ZSet` class)
- **TTL engine** — `Date.now()`-based expiry checked lazily on every access
- **Command parser** — handles quoted strings (`"hello world"`, `'single quoted'`)
- **Pattern matching** — glob-style `KEYS user:*` with `?` and `*` support
- **Type safety** — `WRONGTYPE` errors like real Redis

---

## Limitations (by design)

| Feature | Status |
|---------|--------|
| Data persistence across page reloads | ❌ (in-memory only) |
| MULTI/EXEC transactions | ❌ |
| Pub/Sub | ❌ |
| Lua scripting (EVAL) | ❌ |
| Cluster / replication | ❌ |
| WAIT, OBJECT ENCODING (detailed) | Partial |

---

## License

MIT — do whatever you want with it.
