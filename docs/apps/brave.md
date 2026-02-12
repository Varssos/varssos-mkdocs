# Brave

## Install

```
curl -fsS https://dl.brave.com/install.sh | sh
```

or with flatpak
```
flatpak install flathub com.brave.Browser
```

## Issues

### High cpu temperature (~90) when watching YT, 30-40% frame drops
Issue: Brave can't use graphics acceleration

Fix:

1. Check Graphics acceleration
```
brave://gpu/
```
Expected: most hardware accelerated/enabled
When issue: software only/disabled

2. Check 
```
brave:://settings/system
```
-> Use graphics acceleration when available

3. If issue still visible 
    - Try downgrade brave browser or install from different place(it helped in my case)
    - Remove configs:
```
rm -rf ~/.config/BraveSoftware
rm -rf ~/.cache/BraveSoftware
```


