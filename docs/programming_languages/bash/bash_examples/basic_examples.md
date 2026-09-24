# Basics

## Create script with shebang
```bash
echo "#!"$(which bash) > script.sh
# script.sh contain: #!/usr/bin/bash
```

## Declare string variable
```bash
greeting="Welcome"
```

## Retrieve output of command to variable
```bash
user=$(whoami)
```

## Passing variable into another variable/echo
```bash
echo "$greeting back $user!"
```

## Arithmetic operations
```bash
a=2
b=4
echo $[$a + $b]
```

## Parameter expansion

Used when you want to concatenate a string: `${parameter}`.
```bash
user=$(whoami)
output=/tmp/${user}_home_$(date +%Y-%m-%d_%H%M%S).tar.gz
```
