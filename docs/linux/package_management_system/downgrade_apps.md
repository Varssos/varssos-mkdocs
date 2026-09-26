# Downgrade linux apps

When a recent update introduces a bug or regression, you can roll back an apt package to a previously available version.

## Steps

1. Check the currently installed version:

    ```bash
    apt list --installed | grep <package-name>
    ```

2. List available versions from configured repositories:

    ```bash
    apt-cache madison <package-name>
    ```

3. Install the desired older version:

    ```bash
    sudo apt install <package-name>=<version>
    ```

4. Optionally, pin the package to prevent it from being upgraded automatically:

    ```bash
    sudo apt-mark hold <package-name>
    # To unhold later:
    sudo apt-mark unhold <package-name>
    ```

## Example: VS Code

```bash
$ apt list --installed | grep code
code/stable,stable,now 1.129.0-1784074987 amd64 [installed]

$ apt-cache madison code | head
      code | 1.129.0-1784074987 | https://packages.microsoft.com/repos/vscode stable/main amd64 Packages
      code | 1.129.0-1784074987 | https://packages.microsoft.com/repos/code stable/main amd64 Packages
      code | 1.128.1-1784039518 | https://packages.microsoft.com/repos/vscode stable/main amd64 Packages
...

$ sudo apt install code=1.128.1-1784039518
```