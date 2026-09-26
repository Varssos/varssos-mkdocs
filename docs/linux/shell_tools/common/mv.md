# mv

`mv` moves (renames) files and directories.

## Rename a file
```bash
mv old_name.txt new_name.txt
```

## Move files into a directory
```bash
mv file1.txt file2.txt /path/to/target_dir/
```

## Move without overwriting an existing file
```bash
mv -n source.txt /path/to/target_dir/
```

## Move and back up any file that would be overwritten
```bash
mv -b source.txt /path/to/target_dir/
```