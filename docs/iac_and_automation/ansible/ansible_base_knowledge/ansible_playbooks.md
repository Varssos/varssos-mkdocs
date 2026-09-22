# Ansible playbooks

## Run playbook
```bash
ansible-playbook run.yml -K --ask-vault-pass
```

`run.yml`:
```yaml
---
- hosts: all
  become: yes

  tasks:
    - import_tasks: tasks/essential.yml
```

## Tasks, e.g. in `tasks/essential.yml`

### Update packages with dnf
```yaml
- name: Update packages
  dnf:
    name: "*"
    state: latest
```

### Update packages with apt
```yaml
- name: Update packages
  apt:
    update_cache: yes
    upgrade: yes
```

### Install packages
```yaml
- name: Install essential packages
  package:
    packages:
      - vim
      - htop
      - neofetch
      - tmux
      - speedtest-cli
    state: latest
```
