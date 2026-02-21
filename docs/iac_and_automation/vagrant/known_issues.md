# Known issues


## AMD kvm blocks vagrant
```
sudo modprobe -r kvm_amd
sudo modprobe -r kvm
```

## The forward port ... is already in use
It happens if you run vagrant in multiple places

Stop in one place to unlock it in your desired destination
```
vagrant halt
```

## Not set provider
```
vagrant up --provider=virtualbox
# or
sudo apt-get install -y linux-headers-$(uname -r) build-essential dkms
sudo /sbin/vboxconfig
```