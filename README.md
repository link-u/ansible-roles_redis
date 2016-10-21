redis
=========

redisのrole

install_php_redisをtrueにするとphpから使えるようになります。

Requirements
------------

Ubuntu16.04

Role Variables
--------------

```yaml
redis_server:
  bind: 127.0.0.1
  timeout: 30
  tcp_keepalive: 60
  maxclients: 65536
  maxmemory: 1gb

install_php_redis: false
```

Dependencies
------------

None

Example Playbook
----------------

```yaml
    - hosts: servers
      roles:
         - { role: redis, tags: [ "redis" ] }
```

License
-------

BSD

Author Information
------------------

Link-U Inc.
