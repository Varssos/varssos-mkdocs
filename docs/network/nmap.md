# Nmap

Cool tutorial about [nmap](https://securitybeztabu.pl/nmap-jak-sprawdzic-otwarte-porty/)

## Basic scan
```bash
nmap 192.168.0.100
```

## Ping scan
```bash
nmap -sP 192.168.0.100/24
```

## Scan port range
```bash
nmap -p 1000-1500 192.168.0.100
```

## Scan a few ports
```bash
nmap -p 80,443 192.168.0.100
```

## Scan hosts from an input file

Input file `list.txt`:
```
10.0.1.4
192.168.0.1
```

Command:
```bash
nmap -iL list.txt
```
