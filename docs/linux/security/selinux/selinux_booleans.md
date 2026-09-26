
# SELinux Booleans

SELinux booleans are configuration switches that control specific SELinux policy behaviors at runtime without requiring a policy reload.

## Required Tools

Install essential SELinux tools:

```bash
sudo dnf install setools-console
sudo dnf install policycoreutils policycoreutils-python-utils
```

## SELinux Tools Guide

### sesearch
Search for SELinux rules (allow, neverallow, etc.)

### seinfo
Display general policy information: types, roles, classes, etc.

### sediff
Compare two SELinux policies

### seinfoflow
Analyze information flow between domains

### sesearchx
Extended version of sesearch (availability varies by build)

## Managing Booleans

### Viewing Booleans

List all booleans with default and current values:

```bash
getsebool -a
```

Search for specific booleans:

```bash
semanage boolean -l | grep smb
```

### Viewing Boolean Rules

Display rules associated with a specific boolean:

```bash
sudo sesearch -b smbd_anon_write -A
```

**Example output:**
```
allow smbd_t public_content_rw_t:dir { add_name create getattr ioctl link lock open read remove_name rename reparent rmdir search setattr unlink write }; [ smbd_anon_write ]:True
```

### Changing Boolean State

Enable a boolean temporarily (until reboot):

```bash
setsebool smbd_anon_write on
```

Enable a boolean permanently:

```bash
setsebool -P smbd_anon_write on
```

Options:
- `-P` — Persistent (survives reboot)
