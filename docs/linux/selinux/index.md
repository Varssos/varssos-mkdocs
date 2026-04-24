# SELinux

Security-Enhanced Linux (SELinux) is a mandatory access control (MAC) security module for the Linux kernel. This section covers SELinux concepts, configuration, and management.

## Key Concepts

### Core Components

- **Domain** — SELinux security context for processes (initiating process)
- **Type** — SELinux security context for files and resources (target resources)
- **Class** — Object class to which access is provided
- **Permissions** — Specific actions allowed on a class

### Rule Format

SELinux rules define what a domain can do with a type and class:

```
allow <domain> <type>:<class> { <permissions> };
```

**Example:**
```
allow httpd_t httpd_sys_content_t:file { read };
```

## Checking SELinux Status

View security context of files:
```bash
ls -Z /var
```

View security context of processes:
```bash
ps -Zaux
```

View security context of network connections:
```bash
netstat -Ztulen
```

## Modes

### Getting Current Mode

```bash
getenforce
```

### Setting Mode

```bash
setenforce permissive
```

Modes:

- **Enforcing** — SELinux policies are enforced
- **Permissive** — SELinux policies are logged but not enforced
- **Disabled** — SELinux is disabled

## Audit Logging

SELinux messages are sent to the `auditd` process for logging and analysis.

