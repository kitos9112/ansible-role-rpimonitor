# Ansible Role: RPI-Monitor for Raspberry Pi/s

[Travis-CI]

This Ansible role aims at installing and configuring [RPi Monitor](https://github.com/XavierBerger/RPi-Monitor) utilising as development platform a Raspberry Pi 3B and 4B.

RPi-Monitor allows serving real-time monitoring information (Uptime, CPU load, Temperature, Memory, Disk size, etc...) from your embedded raspberry Pi devices via HTTP in a non-standard port.

Further documentation [here](https://xavierberger.github.io/RPi-Monitor-docs/index.html)

`Data is served over plain-text (HTTP only) and there might be other unkown exploits given the age of this project (last update). Thus I would not recommend openning ports to access data through the internet without properly configuring a VPN tunnel for example.`

## Requirements

- Ansible 2.7+
- Linux Distribution:
  - Raspian Debian Family

A reachable set of Raspberry Pi/s over SSH bootstrapped already (ready to run Ansible modules configured with **password-less sudo user**, e.g. `pi` user comes preconfigured this way by default)

## Role Variables

The following variables could be setup externally and are self-explanatory

```yaml
[defaults](defaults/main.yml)
rpimonitor_user: rpimonitor
rpimonitor_group: rpimonitor
rpimonitor_port: 8888
rpimonitor_ip_addr: 0.0.0.0
```

## Dependencies

There are no other dependencies necessary to run this playbook

## Example Playbook

A simplistic approach to this role.

```yaml
---
# default playbook.yml
- hosts: raspberry_pi
  roles:
      - kitos9112.rpimonitor
```

```shell
# default inventory hosts file
$> cat hosts
#(...)
[raspberry_pi]
  rpi_master-01 ansible_host=192.168.1.101
  rpi_master-02 ansible_host=192.168.1.102
  rpi-slaves-0[1-5] ansible_host=192.168.1.11[0-5]
#(...)
```

CLI command to fire off:

`$> ansible-playbook -i hosts playbook.yml -l raspberry_pi`

## License

MIT || BSD

## Author Information

Role created in 2020 by Marcos S. in a first attempt to start contributing back to the Ansible Galaxy community.

## RPi Monitor official website and code base

RPi monitor is developed by Xavier Berger - source code can be found on [GitHub](https://github.com/XavierBerger/RPi-Monitor)

