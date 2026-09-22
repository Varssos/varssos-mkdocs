# Input, Output and Error Redirections

## stdout redirection
```bash
ls -l > stdout.txt
```

## stderr redirection
```bash
ls -l 2> stderr.txt
```

## stdout and stderr redirection
```bash
ls -l &> stdoutandstderr.txt
```

## Redirect stderr to /dev/null
```bash
tar -czf $output $input 2> /dev/null
```

## Redirect text from file to stdin
```bash
echo "1234" test
cat < test
```

## Passing yes as user input to a command

[More details about automatically responding to a command](https://askubuntu.com/questions/338857/automatically-enter-input-in-command-line)
```bash
printf 'y' | mkfs.ext4 -L sd_card /dev/sda1
# Or use the built-in `yes` command
yes | mkfs.ext4 -L sd_card /dev/sda1
```
