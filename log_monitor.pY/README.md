 # Log_monitor.py

A Python script to monitor a log file in real-time for suspicious entries containing keywords like 'failed', 'unauthorized', or 'invalid'.

Author: codex

GitHub: https://github.com/shadowcodexx

# Script Characteristics:

1. Purpose: Monitor specified log file in real-time to detect suspicious entries.z2. Use Case: Detects unauthorized access or brute-force attempts.
2. Language: Python
3. Libraries: time
4. Monitored File: sample_log.txt
5. Keywords: failed, unauthorized, invalid
6. Functionality:
   Moves to end of file,
   Continuously reads new lines,
   Alerts if suspicious keywords are found
7. Customizable: keywords and log path

```
import time
log_file = "sample_log.txt"
keywords = ["failed", "unauthorized", "invalid"]

with open(log_file, "r") as f:
    f.seek(0, 2)  # Move to the end of the file

    while True:
        line = f.readline()
        if not line:
            time.sleep(0.5)
            continue

        for keyword in keywords:
            if keyword in line.lower():
                print(f"[ALERT] Suspicious log entry: {line.strip()}")
```

