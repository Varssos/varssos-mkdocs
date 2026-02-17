# ansible-vault

[Protecting sensitive data with Ansible vault](https://docs.ansible.com/projects/ansible/latest/vault_guide/index.html)


## How to deal with password in private projects(not fully secure way)
1. Store sensitive data under: `./group_vars/all/secret.yml`
2. Encrypt sensitive data
```
ansible-vault encrypt ./group_vars/all/secret.yml
```

3. Edit it only with
```
ansible-vault edit ./group_vars/all/secret.yml
```

4. Store password to ansible-vault in: `.ansible_vault_pass`
5. Add to `ansible.cfg`:
```
vault_password_file = .ansible_vault_pass
```

6. Add `.ansible_vault_pass` to `.gitignore`

7. Run ansible playbook without passing vault password every time
```bash
ansible-playbook run.yml
```




## Useful ansible-vault cmds

### Decrypt vault
```bash
ansible-vault decrypt ./group_vars/all/secret.yml
```

### View vault content
```bash
ansible-vault view ./group_vars/all/secret.yml
```
