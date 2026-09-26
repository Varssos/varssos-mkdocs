# tar

`tar` bundles (and optionally compresses) files/directories into a single archive.

## Create a compressed archive
```bash
tar -czvf archive.tar.gz /path/to/dir
```
- `-c` create, `-z` gzip, `-v` verbose, `-f` archive file name

## Extract an archive
```bash
tar -xzvf archive.tar.gz -C /path/to/destination
```

## List the contents of an archive without extracting
```bash
tar -tvf archive.tar.gz
```

## Create an archive excluding a directory
```bash
tar -czvf archive.tar.gz --exclude='node_modules' /path/to/dir
```