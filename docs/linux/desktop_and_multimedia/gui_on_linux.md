# GUI on Linux

Nice thread about GUI on Linux is [here](https://unix.stackexchange.com/questions/345344/difference-between-xorg-and-gnome-kde-xfce)

## Terminology

- **Display server** — low-level component (X11/Xorg or Wayland) that draws to the screen and handles input devices.
- **Window manager** — controls window placement, borders, resizing and workspaces (e.g. i3, Mutter).
- **Desktop environment (DE)** — a full suite bundling a window manager, panel, file manager and settings apps (e.g. GNOME, KDE Plasma, XFCE).
- **Display manager** — login screen shown before a session starts (e.g. GDM, LightDM, SDDM); it also lets you pick which session/DE to launch.

## Check what is currently running

```bash
# Is the session X11 or Wayland?
echo $XDG_SESSION_TYPE

# Which desktop environment is active?
echo $XDG_CURRENT_DESKTOP

# Which display manager is active?
systemctl status display-manager
```

## Switching desktop environment / session

Most display managers let you pick the session (GNOME, KDE, XFCE, i3, ...) from a menu on the login screen (usually a gear/settings icon near the password field).
