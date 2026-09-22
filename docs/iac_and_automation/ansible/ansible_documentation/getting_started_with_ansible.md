# Getting started with Ansible

Control node
:   A system on which Ansible is installed.

Managed node
:   A remote system, or host, that Ansible controls.

Inventory
:   A list of managed nodes that are logically organized.

!!! important
    If your managed node (e.g. routers) doesn't have Python, you can only use the `raw` or `script` module. See [this Stack Overflow answer](https://stackoverflow.com/questions/62714153/does-ansible-shell-module-need-python-on-target-server).

1. Install ansible:
```bash
python3 -m pip install --user ansible
sudo apt-get install sshpass
```

2. Create the file `/etc/ansible/hosts`:
```ini
[ubuntu]
192.168.0.62
```

3. Verify the hosts in your inventory:
```bash
ansible all --list-hosts
```

4. Set up an SSH connection to the devices. Create keys, then send the public key to the managed node's `~/.ssh/`.

5. Ping the managed nodes:
```bash
ansible all -m ping -u seba_nas
```

6. Verify disk usage, or run another command, on the managed node:
```bash
ansible ubuntu -m command -a "df -Th" -u seba_nas
```

7. Create a playbook, e.g. `testplay.yml`, as below:
```yaml
---
- hosts: all
  gather_facts: no

  tasks:
    - name: Create file
      ansible.builtin.raw: touch /tmp/file.txt

    - name: Fill data to file.txt
      ansible.builtin.raw: echo "12345" > /tmp/file.txt
```

8. Create a directory `inventory` alongside `testplay.yml`, and add a file `all` to it with this content:
```ini
[openWRT]
192.168.0.101 ansible_user=sshroot ansible_ssh_pass=YOUR_DEVICE_SSH_PASS
```

9. To run the ansible script:
```bash
ansible-playbook -i inventory testplay.yml
```

10. Verify that `/tmp/file.txt` on your device has the following content: `12345`.
