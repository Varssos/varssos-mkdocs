# Bash rules

[Jak wytresowac Basha](https://www.youtube.com/watch?v=fK-CoMVPxxQ)

## Rule: always use quotes

Don't:
```bash
echo $1
echo one two *
```

Do:
```bash
echo "$1"
echo "one two *"
```

Why?
```bash
$ VAR="one two *"

$ echo "${VAR}"
one two *

$ echo ${VAR}
onw two bin boot cdroom dev etc home...
```

## Rule: no space around =

## Rule: assignment quotes

## Rule: immutable globals

- keep them to a minimum
- USE_UPPER_CASE_FORMAT
- make them readonly
