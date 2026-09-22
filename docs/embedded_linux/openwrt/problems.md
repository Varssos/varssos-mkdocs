# Problems on OpenWrt

## File system read only
```
Your JFFS2-partition seems full and overlayfs is mounted read-only.
Please try to remove files from /overlay/upper/... and reboot!
```

1. Check filesystem:
```bash
df -Th
```
2. Check installed packages (some necessary packages e.g python):
```bash
opkg list-installed | grep python
```

3. Uninstall packages:
```bash
opkg remove python3.9
```

4. Find rest bin/.*so files in filesystem:
```bash
find / -name "*python*"
# Output
# /usr/lib/python3.9
# /overlay/upper/usr/lib/python3.9
```

5. Remove files:
```bash
rm /overlay/upper/usr/lib/python3.9
rm /usr/lib/python3.9
```
