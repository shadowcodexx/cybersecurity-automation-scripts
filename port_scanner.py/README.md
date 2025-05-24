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
# Script Characteristics:
1. Purpose: Scans a target IP address or domain for common open ports (22, 80, 443).

2. Language: Python

3. Modules Used: socket (standard library)

4. Input: User enters a domain or IP address.

5. Ports Scanned: 22 (SSH), 80 (HTTP), 443 (HTTPS)

6. Timeout: 1 second per port

7. Output: Prints which of the specified ports are open.

8. Use Case: Quick reconnaissance or validation during network assessments.

9. Execution Type: Interactive command-line script.

10. Requirements: No external dependencies.

11. Platform Compatibility: Cross-platform (Linux, Windows, macOS with Python installed)


