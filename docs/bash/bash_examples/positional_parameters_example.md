# Positional parameters

## Print 1st argument
```bash
echo $1
```

## Print total number of arguments
```bash
echo $#
```

## Print all arguments
```bash
echo $*
```

## Mixing function arguments with script arguments
```bash
function func {
    echo $1
}

echo $1 $2 $4
func $2
# Output of invoking: ./param.sh 1 2 3 4
1 2 4
2
```

Example:
```bash
echo $1 $2 $4   # print 1st argument, 2nd, etc.
echo $#         # print the total number of arguments
echo $*         # print all arguments
# Output of invoking: ./param.sh 1 2 3 4
1 2 4
4
1 2 3 4
```
