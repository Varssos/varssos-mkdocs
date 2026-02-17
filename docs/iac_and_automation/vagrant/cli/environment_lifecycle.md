# Environment lifecycle

[Manage the environment lifecycle](vagrant_environment_lifecycle)

## Saves the current memory state and stops the machine without shutting it down completly
```
vagrant suspend
# Resume:
vagrant resume
```
## Shutdown the machine gracefully (keep files and configs)
```
vagrant halt
```

## Destroy machine
```
vagrant destroy
```

## Remove boxes
```
vagrant box remove hashicorp-education/ubuntu-24-04
```
