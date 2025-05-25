# IP_GeoTracker.py
A Python script to perform geolocation tracking of a given IP address. It uses an external public API to fetch data such as country, city, ISP, and coordinates associated with the IP address.

Author: codex

GitHub: https://github.com/shadowcodexx
```
import requests
def track_ip(ip):
    url = f"http://ip-api.com/json/{ip}"
    try:
        response = requests.get(url, timeout=5)
        data = response.json()
        if data['status'] == 'success':
            print(f"[INFO] IP Address: {ip}")
            print(f"Country: {data['country']}")
            print(f"Region: {data['regionName']}")
            print(f"City: {data['city']}")
            print(f"ZIP: {data['zip']}")
            print(f"Latitude: {data['lat']}")
            print(f"Longitude: {data['lon']}")
            print(f"ISP: {data['isp']}")
            print(f"Org: {data['org']}")
        else:
            print(f"[ERROR] Unable to fetch details: {data['message']}")
    except requests.RequestException as e:
        print(f"[ERROR] Network error: {e}")
if __name__ == "__main__":
    ip_input = input("Enter IP address to track: ")
    track_ip(ip_input)
```
# Characteristics
1. Purpose: Performs IP geolocation tracking to retrieve detailed location and ISP data.
2. Functionality: Queries the ip-api.com API and extracts details like country, region, city, ZIP code, ISP, and coordinates.
3. Input: Accepts an IP address as input from the user via terminal.
4. Output: Displays geolocation information in a clear, labeled format.
5. Modules Used: Utilizes the requests module to interact with the API.
6. Error Handling: Gracefully manages API failures and invalid responses.
7. Timeout: Applies a 5-second timeout to prevent hanging on network issues.
8. Use Case: Useful for cybersecurity analysts, incident responders, or researchers for identifying location-based threat intelligence or attribution.
