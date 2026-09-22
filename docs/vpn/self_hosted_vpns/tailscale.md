# Tailscale

I based on that tutorial to setup my vpn:
[Overcome CGNAT (Carrier-grade NAT) with Tailscale](https://www.youtube.com/watch?v=Sb6eVdF-neA)

## How to install tailscale

```bash
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up --advertise-exit-node --advertise-routes=<YOUR_LOCAL_BROADCAST_IP>/24
# e.g.
sudo tailscale up --advertise-exit-node --advertise-routes=192.168.0.0/24
```

Then you should see link like here:

```
To authenticate, visit:

    https://login.tailscale.com/a/xxxxxxxx

Success.
```

Open this link and login with common account e.g. google account

If you set this on both machine you should see in `Machines` tab your device ip addresses and you should be able to ping in both directions:

```bash
ping 100.x.y.z
```

## How to turn on and turn off tailscale vpn

```bash
sudo tailscale up
sudo tailscale down
```

## Tailscale on Android

You can download tailscale app from google play and login to your common account.

## How install tailscale with ansible

Check github role [here](https://github.com/artis3n/ansible-role-tailscale)

1. Install galaxy role:

```bash
ansible-galaxy role install artis3n.tailscale
```

2. Set tailscale key in env:

```bash
export TAILSCALE_KEY="HERE_YOUR_KEY_FROM_SETTINGS_AUTH_KEYS"
```

3. Set run playbook

```yaml
- name: Servers
  hosts: all
  roles:
    - role: artis3n.tailscale
      vars:
        # Example pulling the API key from the env vars on the host running Ansible
        tailscale_authkey: "{{ lookup('env', 'TAILSCALE_KEY') }}"
        # or
        # tailscale_up_skip: true
```

## How to use subnet routers to have the same ip addresses in tailscale network

[Tailscale subnets](https://tailscale.com/kb/1019/subnets)

In my case I had:

- Laptop with IP address: 192.168.0.64
- Home server with IP address: 192.168.0.63

Both are in the same tailscale network. I just wanted to have the same IP addressing no matter if it is in local network or remotely via tailscale VPN.
To achieve that you should on each device:

1. Install tailscale client
2. Fill `/etc/systemctl.d` with running:

```bash
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
sudo sysctl -p /etc/sysctl.d/99-tailscale.conf
```

3. Allow firewall:

```bash
sudo ufw route allow proto tcp from any to any port 80,443
sudo ufw reload
```

4. Advertise subnet routes and accept routes:

```bash
sudo tailscale up --accept-routes --advertise-routes=192.168.0.0/24
```

5. Enable subnet routes in Machines panel in tailscale. `...` -> `Edit route settings` -> Tick to Enable
