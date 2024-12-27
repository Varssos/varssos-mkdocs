# expect

Expect command or scripting language works with scripts that expect user
inputs. It automates the task by providing inputs.

## Install expect
```
sudo apt install expect
```

## Example

```bash title="que.sh"
#!/bin/bash
echo "Enter your name"
read $REPLY
echo "Enter your age"
read $REPLY
echo "Enter your salary"
read $REPLY
```


```bash title="ans.exp"
#!/usr/bin/expect -f
set timeout -1
spawn ./que.sh
expect "Enter your name\r"
send -- "I am Nikhil\r"
expect "Enter your age\r"
send -- "24\r"
expect "Enter your salary\r"
send -- "100k\r"
expect eof
```

Run expect script:

```bash
chmod +x ./ans.exp
./ans.exp
# Output
spawn ./que.sh
Enter your name
I am Nikhil
Enter your age
24
Enter your salary
100k
```
    

## Autoexpect
You can generate once a expect file which will behave every time. Just
type:

    autoexpect ./que.sh  


## Expect common use cases

### Main expect keywords

| Command      | Function                          |
| -----------  | ------------------------------------ |
| `spawn`      | Creates a new process  |
| `send`       | Sends a reply to the program |
| `expect`     | Wait for output |
| `interact`   | Enables interacting with the program |

### On top you should include

```bash
#!/usr/bin/expect
```

    

### Setting timeout for reaction

```bash
set timeout -1
```

    

### Set internal variable

```bash
set PATH "/home/user/Documents/"
```

    

### Set internal variable from argument

```bash
set FILE [lindex $argv 0] # It starts counting from 0
```

    

### Get password

```bash
stty -echo
send_user -- "Password: "
expect_user -re "(.*)\n"
send_user "\n"
stty echo
set PASS $expect_out(1,string)
send -- "Password was captured\r"
```



### Get text input from user

```bash
send_user "Enter device SN: "
expect_user -re "(.*)\n"
set DEVICE_SN $expect_out(1,string)
send_user "Received SN: $DEVICE_SN\n"
```



### Send file via SCP

```bash
spawn scp $FILE $HOST:$PATH
expect "$HOST's password:";
send "$PASS\r"
```



### Run script on remote server with 1 argument($FILE)

```bash
spawn ssh -t $HOST '/home/user/script.sh' $FILE 
expect "$HOST's password:";
send "$PASS\r"
```



### Hide spawn command in stdout


In case when you invoke script or anything else with spawn you can hide it in stdout like here

```
log_user 0      # Disable logging to stdout
spawn script.sh # Invoke script which shouldn't be visible
log_user 1      # Enable logging to stdout
```


### End expect file with

```bash
expect eof
```
