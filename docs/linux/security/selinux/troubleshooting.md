# Troubleshooting and Debugging SELinux

## Generic Troubleshooting Procedure

1. **Confirm SELinux is the issue**: Temporarily disable enforcement
   ```bash
   setenforce 0
   ```
   Try the failing operation again. If it works, SELinux is blocking it.

2. **Analyze the logs**: Review denial messages in `/var/log/audit/audit.log`

3. **Form a hypothesis**: Based on log analysis, determine what policy changes are needed

4. **Verify with sealert**: Use `sealert` output to confirm your analysis

## AVC Logs

AVC (Access Vector Cache) denials are logged in the audit log when SELinux blocks an action.

### Finding AVC Logs on Red Hat Family Distributions

```bash
sudo grep AVC /var/log/audit/audit.log
```

**Example output:**
```
type=USER_AVC msg=audit(1776789515.350:755): pid=700 uid=81 auid=4294967295 ses=4294967295 subj=system_u:system_r:system_dbusd_t:s0-s0:c0.c1023 msg='avc:  received policyload notice (seqno=2)  exe="/usr/bin/dbus-daemon" sauid=81 hostname=? addr=? terminal=?'UID="dbus" AUID="unset" SAUID="dbus"
```

### Analyzing Log Fields

Key fields in AVC denial messages:

- **pid** — Process ID of the action initiator
- **comm** — Command name executed by the initiator
- **path** — File path accessed by the initiator
- **dev** — Storage device containing the path
- **ino** — Inode number of the accessed file
- **scontext** — Security context of the initiator (source)
- **tcontext** — Security context of the target
- **tclass** — Type of target object (e.g., file, dir, socket)
- **permissive** — Boolean indicating if system was in permissive mode

## Understanding SELinux Rules

### Rule Format

```
allow <domain> <type>:<class> { <permissions> };
```

**Example:**
```
allow user_t var_log_t:dir { getattr search open read };
```

- **user_t** — Domain (actor/process)
- **var_log_t** — Target type (resource)
- **dir** — Class (object type)
- **{ getattr search open read }** — Permissions granted

## Dontaudit Rules

Dontaudit rules suppress logging of certain denials to reduce noise in audit logs.

### Managing Dontaudit Rules

View enforcement statistics including dontaudit:
```bash
seinfo | grep audit
```

Temporarily show suppressed dontaudit rules:
```bash
semanage dontaudit off
```

Search for rules flagged as dontaudit:
```bash
sesearch --dontaudit
```

## Querying Policy Rules

### seinfo — Display SELinux Objects

Query information about SELinux policy:

```bash
seinfo
```

List all available types:
```bash
seinfo -t
```

List all users:
```bash
seinfo -u
```

List all roles:
```bash
seinfo -r
```

List all booleans:
```bash
seinfo -b
```

Get counts for all policy objects:
```bash
seinfo | grep audit
```

### sesearch — Search Policy Rules

Search for rules in the policy and query relationships between source and target:

Show what a domain is allowed to access:
```bash
sesearch -s sshd_t -A
```

Show source domains allowed to access a target:
```bash
sesearch -t public_content_t -A
```

Search specific source and target interaction:
```bash
sesearch -s vmware_t -t public_content_t -A
```

Search for rules related to a boolean:
```bash
sesearch -b ftpd_full_access -A
```

Query what a specific domain can do with a specific target:
```bash
sesearch -s auditd_t -t var_t -A
```

Search by class and permission:
```bash
sesearch -c process -p transition -A
```

## Domain Transitions

A domain transition occurs when a process running in one domain executes a binary and the child process runs in a different domain.

Search for all transition rules:
```bash
sesearch -c process -p transition -A
```

For a domain transition to occur, three conditions must be met:

1. **Execute permission** — The source domain must have the `execute` permission on the executable file:
   ```bash
   sesearch -s sshd_t -t sshd_exec_t -c file -p execute -A
   ```

2. **Entrypoint permission** — The file type must be defined as an entrypoint for the target domain (links the executable to the new domain):
   ```bash
   sesearch -s sshd_t -t sshd_exec_t -c file -p entrypoint -A
   ```

3. **Transition permission** — The source domain must be explicitly allowed to transition to the target domain:
   ```bash
   sesearch -s sshd_t -t sshd_exec_t -c file -p transition -A
   ```

## Generating Policy Rules

### audit2allow — Generate Allow Rules

Convert AVC denial messages into policy rules:

```bash
cat httpd_denied.log | audit2allow -M myhttp
```

This creates:
- `myhttp.pp` — Compiled policy module
- `myhttp.te` — Policy text file

**Best practice**: Use `audit2why` before `audit2allow` to understand denials:
```bash
audit2why < httpd_denied.log | audit2allow -M myhttp
```

### Installing Generated Modules

Load a compiled policy module:

```bash
semodule -i myhttp.pp
```

## Helpful Commands

Check for security alerts in system journal:
```bash
sudo journalctl -xe | grep sealert
```

View detailed alert information:
```bash
sealert -l <LOOKUP_ID>
```

## Context Management Tools

### chcon vs restorecon vs semanage fcontext

- **chcon** — Set the context to the filesystem only (temporary)
- **restorecon** — Relabel the file when needed (persistent with proper policy)
- **semanage fcontext** — Modify SELinux file context policy (persistent)

Use `semanage fcontext` for permanent context changes that will persist across relabeling.