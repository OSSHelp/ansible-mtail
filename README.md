# mtail

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/mtail/status.svg)](https://drone.osshelp.ru/ansible/mtail)

Ansible role that installs and configures mtail-exporter.

## Usage (example)

``` yaml
    - role: mtail
      units:
       - name: dpkg
         target_log: "/var/log/dpkg.log"
         port: 3903
         parsing_params:
           - total_dpkg:
             help: "simple line counter in dpkg.log"
             counter: total_dpkg
             regular: '/$/'
             act: 'total_dpkg++'
           - custom:
             help: "custom counter in dpkg.log"
             counter: 'counts by count_type'
             regular: '/^\d+-\d+.+?\s(?P<count_type>\w{3,5})/'
             act: 'counts[$count_type]++'
        - name: cloud-init
          target_log: "/var/log/cloud-init.log"
          port: 3904
          parsing_params:
            - total_cloud:
              help: "simple line counter in cloud-init.log"
              counter: total_cloud
              regular: '/$/'
              act: 'total_cloud++'
```

## Available parameters

### Global settings and defaults

| Param | Default | Description |
| -----------| ----------- | ----------- |
| `mtail_setup` | `full` | Setup mode. [See OSSHelp KB article](https://oss.help/kb4895). |
| `mtail_exporter_version` | `v3.0.0-rc38` | Version used. Еhe full list can be found on [github page](https://github.com/google/mtail/releases). |

### Available units parameters

| Param | Description |
| ------| ----------- |
| `name` | Name of custom units and config file. |
| `target_log` | The log that the utility parses.  |
| `port` | Listening port. |
| `parsing_params` | Parameters of parsing. |

### Available counts_type parameters

| Param | Description |
| ------| ----------- |
| `help` | Description. |
| `counter` | Metric counter. |
| `regular` | Regular expression. |
| `act` | Action on regex match. |

## FAQ

### Multilog parsing

For parsing several logs at once, a separate instance of a systemd unit with a separate config is created.

## Useful links

- [Official documentation](https://github.com/google/mtail)
- [Our article](https://oss.help/kb7147)

## TODO

...

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
