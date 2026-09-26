# Managing SELinux Contexts

## Changing Contexts with chcon

Change the security context of files:

```bash
chcon -t httpd_sys_content_t /tmp/chconfile
chcon -t httpd_sys_content_t /etc/hosts
```

Options:
- `-t` — Change type
- `-R` — Recursive (with `restorecon`)

## Restoring Default Contexts

Restore SELinux file contexts to their default values:

```bash
restorecon -Rv /tmp
```

Options:
- `-R` — Recursive
- `-v` — Verbose output
- `-F` — Force reset (ignore preexisting digest)

## Port Management

Add or modify port contexts:

```bash
semanage port -a -t http_port_t -p tcp 82
semanage port -m -t http_port_t -p tcp 82
```

Options:
- `-a` — Add a new port mapping
- `-m` — Modify an existing port mapping
- `-t` — Specify the SELinux type
- `-p` — Specify the protocol (tcp/udp)
