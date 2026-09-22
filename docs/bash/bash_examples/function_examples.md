# Functions

## Base syntax
```bash
#!/usr/bin/bash

function user_details {
    echo "User Name: $(whoami)"
    echo "Home Directory: $HOME"

}

user_details
```

## Function arguments
```bash
function your_name {
    echo "Your name is: $1"
}

your_name Chad
```

!!! important
    `$0` in a function means the file name.

## Function which counts files in the current path
```bash
function total_files {
        find $1 -type f | wc -l
}

echo -n "Files in the current path:"
total_files .
```
