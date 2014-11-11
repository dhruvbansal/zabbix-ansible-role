This is an [Ansible](http://www.ansible.com/home) role for installing
[Zabbix agent](https://www.zabbix.com/documentation/2.0/manual/concepts/agent).

You may also be interested in:

* an Ansible role for
  [Zabbix server](https://github.com/dhruvbansal/zabbix-server-ansible-role)
* an Ansible role for the
  [Zabbix frontend](https://github.com/dhruvbansal/zabbix-web-ansible-role)

# What it Does

## Software

Installs the `zabbix-agent` package which provides the following
commands:

* `zabbix_agentd` -- lightweight Zabbix agent process
* `zabbix_agent` -- active version of agent
* `zabbix_sender` -- used to send data to Zabbix server

## Configuration & Logging

Creates the files:

* `/etc/zabbix/zabbix_agentd.conf` -- configuration file for Zabbix agent
* `/etc/logstash/conf.d/zabbix-agent.conf` -- input file for logstash
* `/var/log/zabbix-agent` -- log directory

## Services

Leaves a service `zabbix-agent` running on port 10050.

# Usage

Use the role in a playbook like this:

```yaml
- hosts: all
  roles:
    - zabbix-agent
```

Set the `zabbix_agent_use_logstash` to `false` to skip the logstash
configuration.

## Variables

The following variables are exposed for configuration

* `zabbix_server_host` -- IP address of the Zabbix server the Zabbix agent will accept connections from (also applied for active agents)
* `zabbix_agent_enable_remote_commands` -- set to `1` to allow Zabbix agent to evaluate remote commands sent from Zabbix server
* `zabbix_agent_unsafe_user_parameters` -- set to `1` to allow Zabbix agent to evaluate "unsafe" user parameters
* `zabbix_user_parameters` -- list of user parameters, e.g -
```yaml
zabbix_user_parameters:
  - key: ping[*]
    command: ping $1
  - key: ls[*]
    command: ls $1
```
* `zabbix_agent_hostname` -- override the default hostname picked up by the Zabbix agent
* `zabbix_agent_metadata` -- optional metadata used during host registration
* `zabbix_agent_metadata_item` -- optional item to obtain metadata used during host registration
* `zabbix_agent_use_logstash` -- set to `false` to skip logstash configuration
