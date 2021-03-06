# redis

![ansible ci](https://github.com/link-u/ansible-roles_redis/workflows/ansible%20ci/badge.svg)

## 1. 目次

<!-- TOC depthFrom:2 -->

- [1. 目次](#1-目次)
- [2. 概要](#2-概要)
- [3. 動作確認バージョン](#3-動作確認バージョン)
- [4. 使い方 (ansible)](#4-使い方-ansible)
    - [4.1. Role variables](#41-role-variables)
    - [4.2. Example Playbook](#42-example-playbook)
- [6. License](#6-license)

<!-- /TOC -->

## 2. 概要

redis-server をインストールする role

<br>

## 3. 動作確認バージョン

* Ubuntu: 20.04
* ansible: 2.8, 2.9

<br>

## 4. 使い方 (ansible)

### 4.1. Role variables

```yaml
### インストール設定 ###############################################################################
## 基本設定
redis_install_flag: True # インストールフラグ
redis_conf_path: "/etc/redis/redis.conf"


### conf ファイル設定 ##############################################################################
## INCLUDES
redis_conf_include: null     # null を指定すると conf ファイルには記入されない
## MODULES
redis_conf_loadmodule: null  # null を指定すると conf ファイルには記入されない

## conf ファイルのデフォルト値
#  * デフォルト値としてインストールした直後の値を参考に選んでいる.
redis_conf: 
  bind: "127.0.0.1 ::1"
  protected-mode: "yes"
  port: "6379"
  tcp-backlog: "511"
  timeout: "0"
  tcp-keepalive: "300"
  daemonize: "yes"
  supervised: "no"
  pidfile: "/var/run/redis/redis-server.pid"
  loglevel: "notice"
  logfile: "/var/log/redis/redis-server.log"
  databases: "16"
  always-show-logo: "yes"
  save:
    - "900 1"
    - "300 10"
    - "60 10000"
  stop-writes-on-bgsave-error: "yes"
  rdbcompression: "yes"
  rdbchecksum: "yes"
  dbfilename: "dump.rdb"
  dir: /var/lib/redis
  replica-serve-stale-data: "yes"
  replica-read-only: "yes"
  repl-diskless-sync: "no"
  repl-diskless-sync-delay: "5"
  repl-disable-tcp-nodelay: "no"
  replica-priority: "100"
  replicaof: null   # null を指定すると conf ファイルには記入されない
  lazyfree-lazy-eviction: "no"
  lazyfree-lazy-expire: "no"
  lazyfree-lazy-server-del: "no"
  replica-lazy-flush: "no"
  appendonly: "no"
  appendfilename: '"appendonly.aof"'
  appendfsync: "everysec"
  no-appendfsync-on-rewrite: "no"
  auto-aof-rewrite-percentage: "100"
  auto-aof-rewrite-min-size: "64mb"
  aof-load-truncated: "yes"
  aof-use-rdb-preamble: "yes"
  lua-time-limit: "5000"
  slowlog-log-slower-than: "10000"
  slowlog-max-len: "128"
  latency-monitor-threshold: "0"
  notify-keyspace-events: '""'
  hash-max-ziplist-entries: "512"
  hash-max-ziplist-value: "64"
  list-max-ziplist-size: "-2"
  list-compress-depth: "0"
  set-max-intset-entries: "512"
  zset-max-ziplist-entries: "128"
  zset-max-ziplist-value: "64"
  hll-sparse-max-bytes: "3000"
  stream-node-max-bytes: "4096"
  stream-node-max-entries: "100"
  activerehashing: "yes"
  client-output-buffer-limit:
    - "normal 0 0 0"
    - "replica 256mb 64mb 60"
    - "pubsub 32mb 8mb 60"
  hz: "10"
  dynamic-hz: "yes"
  aof-rewrite-incremental-fsync: "yes"
  rdb-save-incremental-fsync: "yes"
```

<br>

### 4.2. Example Playbook

```yaml
- hosts:
    - servers
  become: True
  roles:
    - { role: redis, tags: ["redis"] }
```

<br>

## 6. License
MIT
