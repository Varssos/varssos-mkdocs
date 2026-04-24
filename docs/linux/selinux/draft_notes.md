# Draft Notes

*(Content moved to individual documentation files)*

See:

- [index.md](index.md) — SELinux basics and concepts
- [acronyms.md](acronyms.md) — SELinux acronyms and abbreviations
- [managing_contexts.md](managing_contexts.md) — Managing SELinux contexts and ports
- [troubleshooting.md](troubleshooting.md) — Troubleshooting, debugging, and AVC logs
- [selinux_booleans.md](selinux_booleans.md) — SELinux booleans and policy tools
- [selinux_modules.md](selinux_modules.md) — SELinux module management and custom modules
- [selinux_users.md](selinux_users.md) — SELinux users and user restrictions








MLS
security from s0-s15

User that has clearence level s3 
- can read files with level s0 to s3
- can not read files with s4 and higher
- can only modify files with the sensivity level s3