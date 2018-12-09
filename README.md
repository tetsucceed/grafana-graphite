### Simple example of using graphite & grafana inside docker.

Usage:

```sh
git clone https://github.com/tetsucceed/grafana-graphite.git
cd grafana-graphite
docker-compose up -d
```

Grafana will access on http://localhost:3000

Graphite will access on http://localhost:7080

---

### On hosts (Centos 7+)

```sh
yum install collectd
```

Then edit */etc/collectd.conf*

Uncomment
```
LoadPlugin write_graphite
...

<Plugin write_graphite>
  <Node "name">
    Host "GRAPHITE_HOST"
    Port "2003"
    Protocol "tcp"
    ReconnectInterval 0
    LogSendErrors true
    Prefix "collectd"
    Postfix "_"
    StoreRates true
    AlwaysAppendDS false
    EscapeCharacter "_"
    SeparateInstances false
    PreserveSeparator false
    DropDuplicateFields false
  </Node>
</Plugin>

```
---

### Troubleshoots

If collectd doesn't start with *Permission denied* on connection with graphite

```sh
audit2allow -a
audit2allow -a -M collectd_t
semodule -i collectd_t.pp
```
