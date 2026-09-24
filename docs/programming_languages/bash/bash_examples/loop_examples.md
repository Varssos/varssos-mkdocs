# Loop examples

## For loop
```bash
for i in 1 2 3; do
    echo $i
done

# Or:

for i in 1 2 3
do
    echo $i
done
```

## For loop example

`items.txt`:
```
bash
scripting
tutorial
```

```bash
for i in $( cat items.txt )
do
    echo -n $i | wc -c
done

# Output:
4
9
8
```

## Print number of characters for all files and directories inside the current working directory
```bash
files=$(ls)
for i in $files
do
    echo "$i has $(printf $i | wc -c)"
done
```

## While loop
```bash
counter=0
while [ $counter -lt 3 ]
do
    let counter+=1
    echo $counter
done
# Output:
1
2
3
```

## Until loop
```bash
counter=6
until [ $counter -lt 3 ]
do
    let counter-=1
    echo $counter
done
# Output:
5
4
3
2
```
