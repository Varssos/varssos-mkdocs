# JPEG files recovery


## Steps to check during recovering jpeg files

1. Get brief analyse from exiftool
```
$ exiftool ./DSC00707.JPG 
ExifTool Version Number         : 12.76
File Name                       : DSC00707.JPG
Directory                       : .
File Size                       : 727 kB
File Modification Date/Time     : 2008:04:27 18:13:00+02:00
File Access Date/Time           : 2026:01:04 12:20:13+01:00
File Inode Change Date/Time     : 2025:12:25 12:51:13+01:00
File Permissions                : -rwxr-xr-x
Error                           : File format error
```

2. Check file entropy. First segments(headers) should have lower entropy. Image(SOS segment) should be close to 1.
```
binwalk -E ./DSC00707.JPG
```

3. Check segment headers

SOI
```
ffd8
```

APP1
```
ffe1
```

SOS
```
ffda000c0301
```

EOI
```
ffd9
```

DHT
```
grep -oba $'\x73\x74\x75\x76\x77' ./*
```

check_ffd8_ffd9.sh
```bash
#!/usr/bin/env bash

shopt -s nullglob

for f in *.jpg *.jpeg *.JPG *.JPEG; do
  [[ -f "$f" ]] || continue

  head_hex=$(xxd -p -l 2 "$f" 2>/dev/null)
  tail_hex=$(xxd -p "$f" 2>/dev/null | tail -n 1)

  if [[ "$head_hex" == "ffd8" || "$tail_hex" =~ ffd9 ]]; then
    echo "=============================="
    echo "FILE: $f"

    if [[ "$head_hex" == "ffd8" ]]; then
      echo "-> Beginning (SOI FFD8):"
      xxd -l 32 "$f"
    else
      echo "-> Beginning (missing FFD8):"
      xxd -l 32 "$f"
    fi

    if [[ "$tail_hex" =~ ffd9 ]]; then
      echo "-> End (EOI FFD9):"
      xxd "$f" | tail -n 4
    else
      echo "-> End (missing FFD9):"
      xxd "$f" | tail -n 4
    fi
  fi
done
```





