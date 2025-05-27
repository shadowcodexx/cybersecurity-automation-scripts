# Hash_identifier.py
A Python script to identify the possible hash type of a given hash string by matching it against common hash regex patterns.

Author: codex

GitHub: https://github.com/shadowcodexx
```
import re

def identify_hash(hash_str):
    hash_patterns = {
        "MD5" : r"^[a-fA-F0-9]{32}$",
        "SHA1": r"^[a-fA-F0-9]{40}$",
        "SHA256": r"^[a-fA-F0-9]{64}$",
        "SHA512": r"^[a-fA-F0-9]{128}$",
        "NTLM": r"^[a-fA-F0-9]{32}$",
        "bcrypt": r"^\$2[aby]?\$[0-9]{2}\$[./A-Za-z0-9]{53}$",
        "LM Hash": r"^[A-F0-9]{32}$",
        "MySQL v3": r"^[a-f0-9]{16}$",
        "MySQL v5+": r"^\*[A-F0-9]{40}$"
    }
    print(f"\n[INFO] Analyzing hash: {hash_str}")
    found = False
    for name, pattern in hash_patterns.items():
        if re.fullmatch(pattern, hash_str):
            print(f"[MATCH] Possible hash type: {name}")
            found = True
    if not found:
        print("[NO MATCH] Hash type could not be identified.")

if __name__ == "__main__":
    input_hash = input("Enter the hash string: ").strip()
    identify_hash(input_hash)
```

# Characteristics
1. Purpose: Identifies common hash types by matching a user-provided hash string against known hash patterns.

2. Functionality: Uses regex matching to compare the input hash with patterns of MD5, SHA variants, NTLM, bcrypt, LM, and MySQL hashes.

3. Input: Accepts a single hash string from user input.

4. Output: Prints the possible hash type(s) or indicates if no match is found.

5. Modules Used: Uses Python’s built-in re module for regular expressions.

6. Error Handling: Gracefully handles unmatched patterns by informing the user.

7. Use Case: Useful for forensic analysis, penetration testing, and cryptanalysis when you need to quickly identify the hash algorithm used.

8. Easy to Extend: New hash types and patterns can be added to the dictionary as needed.

