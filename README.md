# Ansible Role: VNC-Server

Installs [noVNC](https://novnc.com/) & fabric for cyberrange remote access.

## Requirements

- Ansible 2.10+
- Debian-based linux-distribution

## Dependencies

None.

## Role Variables

```yaml
server_name: "novnc"
```

```yaml
novnc_listen: "80"
```

```yaml
novnc_listen_ssl: "443 ssl"
```

```yaml
novnc_upstreams: []
```

## Configuration example

```yaml
- name: Configure noVNC Server
  hosts: novnc
  tasks:
    - name: Set novnc_upstream hosts
      set_fact:
        novnc_upstreams: "{{ novnc_upstreams|default([]) + [{'name': item, 'address': hostvars[item]['ansible_default_ipv4']['address']}] }}"
      with_items: "{{ groups['clients'] }}"

    - name: Configure noVNC Server
      include_role:
        name: novnc
```

## Licence

GPL-3.0

## Author information

Benjamin Akhras
