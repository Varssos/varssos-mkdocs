# ansible-vault

[Protecting sensitive data with Ansible vault](https://docs.ansible.com/projects/ansible/latest/vault_guide/index.html)

[Ansible playbooks secrets (Red Hat)](https://www.redhat.com/sysadmin/ansible-playbooks-secrets)

## Basic vault workflow in a project (not fully secure, but convenient)

1. Store sensitive data under `./group_vars/all/secret.yml`.
2. Encrypt the sensitive data:
```bash
ansible-vault encrypt ./group_vars/all/secret.yml
```

3. Only edit it through `ansible-vault` from now on:
```bash
ansible-vault edit ./group_vars/all/secret.yml
```

4. Store the vault password in `.ansible_vault_pass`.
5. Point `ansible.cfg` to that password file:
```
vault_password_file = .ansible_vault_pass
```

6. Add `.ansible_vault_pass` to `.gitignore` so the password is never committed.
7. Run the playbook without having to pass the vault password every time:
```bash
ansible-playbook run.yml
```

### Alternative: ask for the password interactively

If you don't want to keep a password file on disk, skip `vault_password_file` in `ansible.cfg` and pass `--ask-vault-pass` instead:
```bash
ansible-playbook run.yml --ask-vault-pass
```

## Useful ansible-vault commands

### Create a new vault file
```bash
ansible-vault create secret.yml
```

### Encrypt an existing file
```bash
ansible-vault encrypt api_key.yml
```

### Edit a vault file
```bash
ansible-vault edit ./group_vars/all/secret.yml
```

### Decrypt a vault file
```bash
ansible-vault decrypt ./group_vars/all/secret.yml
```

### View vault content
```bash
ansible-vault view ./group_vars/all/secret.yml
```
