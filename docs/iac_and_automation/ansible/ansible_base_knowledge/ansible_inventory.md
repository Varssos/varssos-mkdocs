# Ansible inventory

- Default location for the inventory is `/etc/ansible/hosts`.
- You can specify a different inventory with `-i <path>`.
- Create `ansible.cfg` pointing to the default inventory location:
```ini
[defaults]
INVENTORY = inventory
```

## Basic inventory in INI format
```ini
[ubuntu]
192.168.0.62
192.168.0.63
```

## Inventory with passwords in INI format
```ini
[ubuntu]
192.168.0.62 ansible_user=seba_nas ansible_port=5555 ansible_ssh_pass=YOUR_DEVICE_SSH_PASS
192.168.0.63 ansible_user=seba_nas ansible_port=5555 ansible_ssh_pass=YOUR_DEVICE_SSH_PASS
```

## Inventory with keys
```ini
[ubuntu]
192.168.0.62 ansible_user=seba_nas ansible_ssh_private_key_file=~/.ssh/nas_seba
```

## Inventory in YAML format
```yaml
machines:
  hosts:
    seba_nas:
      ansible_host: 192.168.0.62
      ansible_port: 5555
      ansible_user: seba_nas
```

## Setting `ansible_user` as a group var
```yaml
machines:
  hosts:
    seba_nas:
      ansible_host: 192.168.0.62
      ansible_port: 5555

  vars:
    ansible_user: seba_nas
```

## Using metagroups in the inventory
```yaml
nas:
  hosts:
    seba_nas:
      ansible_host: 192.168.0.62

rpi:
  hosts:
    seba_rpi:
      ansible_host: 192.168.0.60

home_lab:
  children:
    nas:
    rpi:
```
