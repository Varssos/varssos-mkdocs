# USB Hub — Disable Autosuspend for USB Ethernet Adapter

**Goal:** Prevent the USB network card and its parent hub from going into power-saving sleep, which can drop the network connection.

---

## Step 1 — Find the sysfs path of your network card

```bash
readlink -f /sys/class/net/enx00e04c680348/device
```

Expected output: `.../usb2/2-3/2-3.2:1.0`
- Network card device: `2-3.2`
- Parent hub device: `2-3`

> Adjust the device paths in the steps below to match your output.

---

## Step 2 — Disable autosuspend on the network card

```bash
echo "on" | sudo tee /sys/bus/usb/devices/2-3.2/power/control
echo -1   | sudo tee /sys/bus/usb/devices/2-3.2/power/autosuspend_delay_ms
```

---

## Step 3 — Disable autosuspend on the parent hub

```bash
echo "on" | sudo tee /sys/bus/usb/devices/2-3/power/control
echo -1   | sudo tee /sys/bus/usb/devices/2-3/power/autosuspend_delay_ms
```

---

## Step 4 — Verify

```bash
cat /sys/bus/usb/devices/2-3.2/power/control   # expected: on
cat /sys/bus/usb/devices/2-3/power/control      # expected: on
```

---

## Step 5 — Make it persistent across reboots (udev rule)

```bash
sudo tee /etc/udev/rules.d/99-usb-eth-power.rules << 'EOF'
ACTION=="add", SUBSYSTEM=="usb", ATTR{idVendor}=="0bda", ATTR{idProduct}=="8153", ATTR{power/control}="on", ATTR{power/autosuspend_delay_ms}="-1"
ACTION=="add", SUBSYSTEM=="usb", ATTR{idVendor}=="0bda", ATTR{idProduct}=="0411", ATTR{power/control}="on"
EOF
sudo udevadm control --reload-rules
```

> - `0bda:8153` = Realtek RTL8153 network card
> - `0bda:0411` = Generic USB 3.2 hub (`2-3`)

---

## How to find idVendor/idProduct if hardware changes

```bash
# Network card
cat /sys/bus/usb/devices/2-3.2/idVendor
cat /sys/bus/usb/devices/2-3.2/idProduct

# Hub
cat /sys/bus/usb/devices/2-3/idVendor
cat /sys/bus/usb/devices/2-3/idProduct
```

Update the udev rule in Step 5 with the new IDs.