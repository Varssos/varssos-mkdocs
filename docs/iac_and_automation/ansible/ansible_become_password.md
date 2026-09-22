# Ansible become password

## Password in ansible.cfg

Add this to `ansible.cfg`:
```
ansible_become_password = 12345
```

## Hashed password in secrets.yml

1. In `group_vars/all/secrets.yml`:
```yaml
ansible_become_password: 12345
```

2. Encrypt the file:
```bash
ansible-vault encrypt ./group_vars/all/secrets.yml
```

3. In `ansible.cfg`:
```
vault_password_file = pass
```

4. Create the file `pass` and fill in the password:
```bash
echo "12345" > pass
```

5. Run ansible:
```bash
ansible-playbook ./run.yml
```
