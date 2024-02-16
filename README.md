# Script to automate port discovery for a host

```bash
#!/bin/bash
# Must be run as superuser

if [[ -z $1 ]]; then
        echo "Syntax: ./scan.sh <IP>"
else
        folder=$(pwd | awk -F'/' '{print $NF}')
        if [[ ! -d nmap/ ]]; then
                mkdir nmap
        fi
        open_ports=$(nmap -p- $1 | grep open | awk -F'/' '{print $1}' 'ORS=,' | sed 's/.$//')
        echo -e "[*] Ports found: $open_ports"
        echo -e "[*] Starting service scan on host $1"
        nmap -sC -sV -oA nmap/$folder -p$open_ports $1
fi
```
