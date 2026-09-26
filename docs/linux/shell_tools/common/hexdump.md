# Hexdump

[Geeksforgeeks hexdump](https://www.geeksforgeeks.org/hexdump-command-in-linux-with-examples/)

## Display file as hex array

```bash
hexdump -v -e '/1 "0x%02X, "' file_name.zip
```
