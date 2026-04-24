# SELinux Users and Restrictions

## Overview

SELinux users define security contexts for system users. By default, users are mapped to `unconfined_u` which has no restrictions.

## Checking User Context

Check the current SELinux user context:

```bash
id -Z
```

## SELinux User Mappings

View current login to SELinux user mappings:

```bash
sudo semanage login -l
```

Example output:
```
Login Name           SELinux User         MLS/MCS Range        Service

__default__          unconfined_u         s0-s0:c0.c1023       *
root                 unconfined_u         s0-s0:c0.c1023       *
```

## Available SELinux Users

List all available SELinux users on the system:

```bash
seinfo -u
```

Common SELinux users:
- `unconfined_u` — Unrestricted user (default for most users)
- `user_u` — Restricted user with limited privileges
- `staff_u` — Staff/administrator users
- `sysadm_u` — System administrator
- `guest_u` — Guest user (most restrictive)
- `xguest_u` — X11 guest user (browser-only, very restrictive)
- `root` — Root user
- `system_u` — System processes

## User-Specific Booleans

Different user types have associated booleans that control their capabilities:

```bash
getsebool -a | grep -E 'guest|staff|sysad'
```

Example:
```
guest_exec_content --> on
ssh_sysadm_login --> off
staff_exec_content --> on
staff_use_svirt --> off
sysadm_exec_content --> on
xdm_sysadm_login --> off
xguest_connect_network --> on
xguest_exec_content --> on
xguest_mount_media --> on
xguest_use_bluetooth --> on
```

## Creating Users with SELinux Contexts

### Create a Staff User

```bash
useradd -Z staff_u isabelle
```

This creates a new user `isabelle` with the `staff_u` SELinux user context.

### Create a Restricted Kiosk User

Create a user that only has access to a web browser:

```bash
useradd -Z xguest_u limited
```

The `xguest_u` context is the most restrictive and used for guest or kiosk scenarios.

## Role Information

View available roles for a specific SELinux user:

```bash
seinfo -r
```

Example - viewing container user role:

```bash
seinfo -r container_user_r
seinfo -r container_user_r -x
```

This shows the types accessible by the `container_user_r` role, including file types, device types, and other context objects.

## Modifying User Mappings

Add or modify login to SELinux user mappings:

```bash
semanage login -a -s user_u USERNAME
```

Options:
- `-a` — Add a new mapping
- `-d` — Delete a mapping
- `-s` — Specify the SELinux user context
