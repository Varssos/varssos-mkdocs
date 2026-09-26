# find

`find` searches a directory tree for files/directories matching given criteria.

## Move only files ignoring directories

```bash
find /path/to/search -type f -exec mv -t /path/where/to/move {} +
# -t means target
```

## Find files older than N days and delete them

```bash
find /path/to/search -type f -mtime +30 -delete
```


