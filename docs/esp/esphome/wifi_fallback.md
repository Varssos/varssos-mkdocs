# Wifi fallback in esp home

https://esphome.io/components/captive_portal.html

## In case of configured wifi not reachable

1. Connect on laptop/phone to AP e.g. `Esp32-Test Fallback Hotspot`
2. Fill password from config
3. Open in browser: `http://192.168.4.1/` and change SSID and password
4. Save and then device will be restarted. That's all.