# datadog-checks

![Build Status](https://travis-ci.org/traveloka/ansible-datadog-checks.svg?branch=master)

Configure Datadog checks

## Requirements

awslogs is installed

## Role Variables
- datadog_agent_checks_config_dir: datadog checks config directory.
  This default to `/etc/dd-agent/conf.d`
- datadog_checks: DataDog agent checks in YAML configuration that will be dropped into `{{ datadog_agent_checks_config_dir }}`
- datadog_user, datadog_group: The user and group that should own the checks configuration files

## Dependencies

DataDog Agent is installed

## Example Playbook

```
---
- hosts: all
  become: True
  roles:
    - name: ansible-datadog-checks
      datadog_checks:
        jmx:
          init_config: null
          instances:
          -   conf:
              -   include:
                      attribute:
                          Usage.max:
                              metric_type: gauge
                          Usage.used:
                              metric_type: gauge
                      domain: java.lang
                      type: MemoryPool
              -   include:
                      attribute:
                          CollectionCount:
                              metric_type: gauge
                      domain: java.lang
                      type: GarbageCollector
              jmx_url: service:jmx:rmi:///jndi/rmi://127.0.0.1:14928/jmxrmi
              name: jmx-localhost-14928
```

## License

MIT

## Author Information

[Salvian Reynaldi](https://github.com/salvianreynaldi)
