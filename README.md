
# Ansible Role:  `loki`

Ansible role to setup [Loki](https://github.com/grafana/loki).


[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/bodsch/ansible-loki/2.4.x)][ci]
[![GitHub issues](https://img.shields.io/github/issues/bodsch/ansible-loki)][issues]
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/bodsch/ansible-loki)][releases]

[ci]: https://github.com/bodsch/ansible-loki/actions
[issues]: https://github.com/bodsch/ansible-loki/issues?q=is%3Aopen+is%3Aissue
[releases]: https://github.com/bodsch/ansible-loki/releases


## Requirements & Dependencies

- None

### Operating systems

Tested on

* Debian 10 / 11
* Ubuntu 20.10
* CentOS 8
* Oracle Linux 8
* Arch Linux

## usage

### default configuration

```yaml

loki_version: "2.4.1"
loki_release_download_url: https://github.com/grafana/loki/releases

loki_system_user: loki
loki_system_group: loki
loki_config_dir: /etc/loki
loki_storage_dir: /var/lib/loki

loki_listen_address: 127.0.0.1
loki_listen_port: 3100

loki_log:
  level: info

loki_target: all
loki_auth_enabled: true

loki_config_server:
  http_listen_address: "{{ loki_listen_address }}"
  http_listen_port: "{{ loki_listen_port }}"

loki_config_distributor:
  ring:
    kvstore:
      store: inmemory

loki_config_querier: {}

loki_config_ingester:
  lifecycler:
    address: 127.0.0.1
    ring:
      kvstore:
        store: inmemory
      replication_factor: 1
    final_sleep: 0s
  chunk_idle_period: 5m
  chunk_retain_period: 30s
  wal:
    dir: "{{ loki_storage_dir }}/wal"
    enabled: true

loki_config_ingester_client: {}

loki_config_storage:
  boltdb:
    directory: "{{ loki_storage_dir }}/index"
  filesystem:
    directory: "{{ loki_storage_dir }}/chunks"

loki_config_chunk_store:
  max_look_back_period: 0s

loki_config_schema:
  configs:
    - from: 2020-05-15
      store: boltdb
      object_store: filesystem
      schema: v11
      index:
        prefix: index_
        period: 168h
      chunks:
        prefix: index_
        period: 168h
      row_shards: 16

loki_config_limits:
  enforce_metric_name: false
  ingestion_burst_size_mb: 32
  ingestion_rate_mb: 16
  max_query_parallelism: 64
  reject_old_samples: true
  reject_old_samples_max_age: 168h

loki_config_frontend_worker: {}

loki_config_runtime: {}

loki_config_table_manager:
  retention_deletes_enabled: false
  retention_period: 0s

# loki 2.4
loki_config_memberlist: {}

loki_config_compactor:
  working_directory: "{{ loki_storage_dir }}/compactor"
  shared_store: filesystem
  compaction_interval: 5m
```


## Contribution

Please read [Contribution](CONTRIBUTING.md)

## Development,  Branches (Git Tags)

The `master` Branch is my *Working Horse* includes the "latest, hot shit" and can be complete broken!

If you want to use something stable, please use a [Tagged Version](https://gitlab.com/bodsch/ansible-icinga2/-/tags)!

---

## Author and License

- Bodo Schulz

## License

[Apache](LICENSE)

**FREE SOFTWARE, HELL YEAH!**
