# ansible-smartctl_exporter

Role for deploy Prometheus
[smartctl_exporter](https://github.com/prometheus-community/smartctl_exporter)

## Requirements

* Ansible 3.0.0+

Example configuration
-------------------------

```yaml
smartctl_exporter:
  # Install/upgrade exporter package, otherwise binary from Github will
  # be installed
  - install_package: 'true'
  # 'present' (do nothing if package is already installed) or 'latest' (always
  # upgrade to last version)
    package_state: 'latest'
  # version of the exporter in case of Github deployment (not relevant for
  # package deployment): bare value, like '0.8.0' or latest' - the latest
  # release from Github
    version: 'latest'
    # enable exporter service or not
    enable: 'true'
    # restart exporter service or not
    restart: 'true'
    # The configuration of smartctl_exporter
    settings:
      # The path to the smartctl binary"
      - smartctl_path: '/usr/bin/smartctl'
      # The interval between smarctl polls (default is 60s)
        smartctl_interval: '60s'
      # The devices to monitor
        smartctl_device:
          - '/dev/sda'
          - '/dev/nvme0n1'
      # Address to listen on for web interface and telemetry
        web_listen_address: ':9633'
      #  Path under which to expose metrics
        web_telemetry_path: '/metrics'
        log_level: 'info'
      # Output format of log messages. 'logfmt' or 'json'
        log_format: 'logfmt'
```
