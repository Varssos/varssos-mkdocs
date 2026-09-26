# nice

`nice` starts a command with an adjusted scheduling priority. Values range from -20 (highest priority) to 19 (lowest); only root can set negative values.

## Run command with lowest priority
```bash
nice -n 19 CMD
```

## Run command with the highest priority
```bash
nice -n -20 CMD
```
