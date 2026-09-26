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

## Multi-Level Security (MLS)

MLS adds sensitivity levels (`s0`-`s15`) on top of the usual type enforcement, restricting access based on data classification rather than just type. A user/process cleared for a given level can read data at or below that level, but cannot read higher levels and can only modify data at its own level.

Example: a user cleared for level `s3`:

- Can read files with level `s0` to `s3`.
- Cannot read files with level `s4` or higher.
- Can only modify files at sensitivity level `s3`.

