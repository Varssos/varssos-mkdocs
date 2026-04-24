# SELinux Acronyms and Abbreviations

## General

- **SELinux** — Security-Enhanced Linux
- **MAC** — Mandatory Access Control
- **DAC** — Discretionary Access Control

## SELinux Components and Mechanisms

- **AVC** — Access Vector Cache
- **LSM** — Linux Security Module
- **TEAC** — Type Enforcement Access Control
- **RBAC** — Role-Based Access Control
- **TE** — Type Enforcement
- **MCS** — Multi-Category Security
- **MLS** — Multi-Level Security

## Objects and Types

- **SID** — Security ID
- **SELinux context** — SELinux security context (user:role:type:level)
- **Type** — Object type in SELinux

## Modes and Policies

- **Policy** — SELinux security policy
- **Enforcing** — Enforcement mode
- **Permissive** — Permissive mode (logging without blocking)
- **Disabled** — SELinux disabled

## Tools and Commands

- **semanage** — SELinux Policy Management Tool
- **restorecon** — Restore SELinux file contexts
- **getenforce** — Get current SELinux enforcement state
- **setenforce** — Set SELinux enforcement mode
- **audit2why** — Explain SELinux denial
- **audit2allow** — Generate SELinux policy allow rules
