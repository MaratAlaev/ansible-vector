# Ansible Role: vector

Настраивает vector для ваших хостов

## Role Variables

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| vector_version | 0.33.0 | C помощью этой переменной можно изменять версию vector |
| vector_config |  | Переменная устанавливает конфиг для vector |


## Example

### playbook

```yaml
- name: Install Vector to server
  hosts: vector-server, lighthouse
  vars:
    vector_version: "0.33.0"

    vector_config: 
      sources:
        track:
          type: "vector"
          address: "0.0.0.0:9876"

      sinks:
        output_clickhouse:
          type: "clickhouse"
          inputs: ["track"] 
          endpoint: "http://{{ hostvars['clickhouse-01'].ansible_default_ipv4.address }}:8123"
          database: "nginxdb"
          table: "access_logs"
          skip_unknown_fields: true
  roles:
    - {role: vector-role}
```
