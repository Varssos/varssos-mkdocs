# SELinux Modules

## Module Management Commands

### semodule Command

Disable a module:
```bash
sudo semodule -d zabbix
```

Enable a module:
```bash
sudo semodule -e zabbix
```

### Managing Module Priority

Install a module with priority (higher priority takes precedence):
```bash
semodule -X 500 -i mymodule.pp
```

## Writing Custom SELinux Modules

### Basic Workflow

Example: Creating a module named "sander" version 1.0

1. Create the policy file (.te):
   ```bash
   vim sander.te
   ```

2. Create the file contexts (.fc):
   ```bash
   vim sander.fc
   ```

3. Compile the module:
   ```bash
   checkmodule -M -m -o sander.mod sander.te
   ```

4. Package the module:
   ```bash
   semodule_package -o sander.pp -m sander.mod -f sander.fc
   ```

5. Install the module:
   ```bash
   semodule -i sander.pp
   ```

## Additional Tools

- **runcon** — Run a command with a specified SELinux context
- **sepolicy generate** — Generate SELinux policies
