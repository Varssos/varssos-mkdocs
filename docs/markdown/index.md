# Markdown



## Markdown tricks

### Markdown expand hack

<details>
<summary>Procedure</summary>

Generic text

<details>
<summary> Step 1: Check logs</summary>

```bash
journalctl -u my-service
```

<details>
<summary>Additional debugging</summary>

```bash
journalctl -u my-service --since "1 hour ago"
dmesg | tail -n 100
```

</details>

</details>

<details>
<summary>Step 2: Check configuration</summary>

```bash
cat /etc/my-service/config.conf
```

</details>

</details>

### [Icons](https://squidfunk.github.io/mkdocs-material/reference/icons-emojis/)
