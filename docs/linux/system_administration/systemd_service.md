# Systemd service

[How to create a Systemd service in Linux](https://www.shubhamdipt.com/blog/how-to-create-a-systemd-service-in-linux/)

1. Go to `/etc/systemd/system`:
```bash
cd /etc/systemd/system
```

2. Create a file named your-service.service and include the following:
```ini
[Unit]
Description=<description about this service>
After=network.target

[Service]
Type=simple
WorkingDirectory=<directory_of_script e.g. /root>
ExecStart=<script which needs to be executed>
ExecReload=/bin/kill -HUP $MAINPID
Restart=always
StandardOutput=syslog
StandardError=syslog
User=<user>
Group=<user_group>
Environment=PATH=/sbin:/bin:/usr/sbin:/usr/bin:/usr/local/bin


[Install]
WantedBy=multi-user.target
```

3. Reload the service files to include the new service:
```bash
sudo systemctl daemon-reload
```

4. Start your service:
```bash
sudo systemctl start your-service.service
```

5. Check status of your service:
```bash
sudo systemctl status your-service.service
```

6. Enable your service on every reboot:
```bash
sudo systemctl enable your-service.service
```

7. Disable your service on every reboot:
```bash
sudo systemctl disable your-service.service
```
