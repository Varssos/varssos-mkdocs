# swap

## Increase swap from default 2GB to 32 GB (e.g. prevent lack of RAM during building Android)

1. Disable the Current Swap

    ```bash
    sudo swapoff -a
    ```

    This will turn off all swap space temporarily. You can verify that swap is disabled by checking:

    ```bash
    swapon --show
    ```

2. Remove the Existing Swap File (if needed)
    ```bash
    sudo rm /swapfile
    ```
3. Create a New Swap File (32GB)

    ```
    sudo fallocate -l 32G /swapfile
    ```
    Alternatively, if fallocate doesn’t work or you encounter issues, you can use dd to create the swap file:

    ```
    sudo dd if=/dev/zero of=/swapfile bs=1M count=32768
    ```

4. Set Correct Permissions
    ```
    sudo chmod 600 /swapfile
    ```
5. Make the Swap File
    ```
    sudo mkswap /swapfile
    ```
6. Enable the Swap File
    ```
    sudo swapon /swapfile
    ```
7. Verify the New Swap Size
    ```
    swapon --show
    ```


8. Make the Swap File Permanent
    
    To ensure the swap file is used after reboot, add it to /etc/fstab.

    ```
    sudo nano /etc/fstab
    ```
    Add the following line to the end of the file:

    ```
    /swapfile none swap sw 0 0
    ```

9. Re-enable Swap After Reboot (if applicable)
    ```
    sudo reboot
    ```
    After reboot, you can verify that the swap is still enabled and has the correct size by running:

    ```
    swapon --show
    ```
    That's it! You have successfully increased the swap size to 32GB on your Ubuntu system.