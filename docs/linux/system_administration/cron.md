# Cron

A crontab file contains instructions for the cron(8) daemon in the following simplified manner: "run this command at this time on this date".

Useful tool to generate crontab lines: [crontab-generator.org](https://crontab-generator.org)

## Edit cron configuration
```bash
crontab -e
```

## Edit cron configuration for user
```bash
crontab -u sshroot -e
```

## Crontab example

Everyday at 4:00 run `/home/user/command.sh`:
```bash
0 4 * * * /home/user/command.sh
```

## Show configuration
```bash
crontab -l
```

## Apply changes
```bash
service cron restart
```

## at - schedule a one-time job

Unlike cron, `at` schedules a command to run only once at a given time.

```bash
# Schedule a job 3 minutes from now
at now +3 minutes

# List queued at jobs
atq

# Show the command scheduled for job 1
at -c 1
```
