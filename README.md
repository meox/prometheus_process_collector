# Prometheus.io Process Collector
[![Hex.pm](https://img.shields.io/hexpm/v//prometheus_process_collector.svg?maxAge=2592000)](https://hex.pm/packages/prometheus_process_collector)
[![Hex.pm](https://img.shields.io/hexpm/dt/prometheus_process_collector.svg?maxAge=2592000)](https://hex.pm/packages/prometheus_process_collector)
[![Build Status](https://travis-ci.org/deadtrickster/prometheus_process_collector.svg?branch=master)](https://travis-ci.org/deadtrickster/prometheus_process_collector)

Collector which exports the current state of process metrics including cpu, memory, file descriptor usage and native threads count as well as the process start and up times.

- Linux - uses /proc;
- FreeBSD.

## Installation

**Hex package note**: Because OTP strictly validates NIF version c_src was compiled with, I removed precompiled binaries from the Hex package. This means that OTP source code is needed to build this library.

When erlang is running in embedded mode this collector should be picked up automatically. For interactive
mode (i.e. iex, mix, etc) it must be registered manually:

```erlang
prometheus_registry:registry_collector(prometheus_process_collector)
```

```elixir
Prometheus.Registry.register_collector(:prometheus_process_collector)
```

## Example scrape:

```
# TYPE process_open_fds gauge
# HELP process_open_fds Number of open file descriptors.
process_open_fds 11
# TYPE process_max_fds gauge
# HELP process_max_fds Maximum number of open file descriptors.
process_max_fds 20000
# TYPE process_start_time_seconds gauge
# HELP process_start_time_seconds Start time of the process since unix epoch in seconds.
process_start_time_seconds 1469491524
# TYPE process_uptime_seconds gauge
# HELP process_uptime_seconds Process uptime in seconds.
process_uptime_seconds 18
# TYPE process_threads_total gauge
# HELP process_threads_total Process Threads count.
process_threads_total 18
# TYPE process_virtual_memory_bytes gauge
# HELP process_virtual_memory_bytes Virtual memory size in bytes.
process_virtual_memory_bytes 2785275904
# TYPE process_resident_memory_bytes gauge
# HELP process_resident_memory_bytes Resident memory size in bytes.
process_resident_memory_bytes 57053184
# TYPE process_cpu_seconds_total counter
# HELP process_cpu_seconds_total Process CPU seconds total.
process_cpu_seconds_total{kind="utime"} 2.46
process_cpu_seconds_total{kind="stime"} 5.44
```

Usage
-----

You can register this collector manually using `prometheus_process_collector/0,1` or use `default_collectors` env entry for `prometheus`.

With [Prometheus Plugs](https://github.com/deadtrickster/prometheus-plugs) - just add prometheus_process_collector dependency to top-level project (i.e. [like here](https://github.com/deadtrickster/prometheus-plugs-example/edit/master/mix.exs)).

## Integrations / Collectors / Instrumenters
 - [Ecto collector](https://github.com/deadtrickster/prometheus-ecto)
 - [Plugs Instrumenter/Exporter](https://github.com/deadtrickster/prometheus-plugs)
 - [Elli middleware](https://github.com/elli-lib/elli_prometheus)
 - [Fuse plugin](https://github.com/jlouis/fuse#fuse_stats_prometheus)
 - [Phoenix instrumenter](https://github.com/deadtrickster/prometheus-phoenix)
 - [Process Info Collector](https://github.com/deadtrickster/prometheus_process_collector.erl)
 - [Prometheus.erl](https://github.com/deadtrickster/prometheus.erl)
 - [Prometheus.ex](https://github.com/deadtrickster/prometheus.ex)
 - [RabbitMQ Exporter](https://github.com/deadtrickster/prometheus_rabbitmq_exporter)

Build
-----

    $ rebar3 compile

License
-----

FreeBSD-specific part uses copy-modified code from standard utils (limits and procstat) or standard API in some places.

MIT
