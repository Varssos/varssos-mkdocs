# grep

`grep` searches text for lines matching a pattern.

## Search recursively phrase and exclude dir

```bash
grep --exclude-dir=your_dir/ -rn "abc"
```

## Search case-insensitively and show only matching part

```bash
grep -io "abc[a-z]*" file.txt
```


## Search recursively with case insensitive

```bash
grep -rni "abc"
```
