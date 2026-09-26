# Users

Practice exercises for common `useradd`/`usermod`/`groupadd` user and group management tasks.

1. Create an account for user Kermit with a home directory. `sudo useradd -d /home/Kermit -m Kermit`
2. Create an account for user Piggy, but the home directory should be set to /muppety/Piggy. `sudo useradd -d /muppety/Piggy -m Piggy`
3. Create the group muppety. `sudo groupadd muppety`
4. Add users Kermit and Piggy to the group muppety. `sudo usermod -G muppety Kermit`
5. Move Kermit's home directory to /muppety/Kermit. `sudo mv /home/Kermit/ /muppety/`
6. Lock Piggy's password. `sudo usermod -L Piggy`
7. Unlock Piggy's account. `sudo usermod -U Piggy`
8. Change your own password. `sudo passwd $USER`
9. Check your own user ID and the groups you belong to. `id`
10. Check who is currently logged into the system. `w/who/finger`
