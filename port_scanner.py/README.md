# Port_scanner.py


A simple Python script to scan common network ports (22, 80, 443) on a target IP address or domain using the socket library.

Author: codex

GitHub: https://github.com/shadowcodexx

```

import socket

target = input("Enter target IP or Domain: ")

ports = [22, 80, 443]

for port in ports:
    s = socket.socket()
    s.settimeout(1)
    try:
        s.connect((target, port))
        print(f"Port {port} is open")
    except:
        pass
    s.close()
```
