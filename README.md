## Adaptive Request Monitoring System with DDoS Protection

## Overview

This project implements an Adaptive Request Monitoring System using an Arduino with Ethernet capabilities. The system monitors incoming requests and adapts dynamically to detect and respond to potential Distributed Denial-of-Service (DDoS) attacks. When suspicious activity is detected, such as an unusual spike in request rates, the system triggers an alert and can block the offending IP address.
## Feature 

1. Real-time Request Monitoring:

- Tracks the number of incoming requests in real-time.
- Utilizes a rolling average to adjust the detection threshold dynamically.

2. Adaptive Threshold Calculation:

- The system adapts its threshold based on recent activity, making it more sensitive to potential attacks while reducing false positives.

3. Alert System:

- An LED or buzzer connected to pin 7 serves as an alert mechanism when a potential DDoS attack is detected.
4. IP Blocking Mechanism:

- Blocks IP addresses that exceed the adaptive threshold.
- Maintains a block list of up to 10 IP addresses.
## Components 

- Arduino Board with Ethernet Shield
- Ethernet Cable connected to a network with IP address 192.168.1.177
- LED/Buzzer connected to digital pin 7 for alert notifications
## How It Work 

1. Setup:

- The system initializes by setting up the Ethernet connection, server, and alert pin.
- A rolling average array for request samples is initialized.

2. Monitoring Loop:

- The loop continuously checks for client connections.
- If a client connects, the system verifies whether the client's IP is on the block list. If it is, the connection is terminated immediately.
- The number of incoming requests is counted, and data is processed, even if not logged.

3. Adaptive Threshold Adjustment:

- Every second, the system updates the rolling average of requests.
- The adaptive threshold is recalculated as the base threshold plus half of the rolling average.

4. Attack Detection:

- If the request count within the interval exceeds the adaptive threshold, the alert pin is triggered, and the offending IP is blocked.
- The system logs relevant data, including the number of requests and the current threshold, for further analysis.

5. IP Blocking:

- Offending IPs are added to a block list, preventing them from making further requests.
## Configuration 

## Network Configuration
- MAC Address: 0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED
- IP Address: 192, 168, 1, 177
- Server Port: 80
## Adaptive Threshold and Rolling Average
- Base Threshold: 100 requests per second.
- Rolling Average Sample Size: 10 intervals.
- Adaptive Threshold Formula: baseThreshold + (averageRequests * 0.5)
## Alert and Blocking Settings
- Alert Pin: 7 (Can be connected to an LED or buzzer).
- Maximum Block List Size: 10 IP addresses.
## Usage 
- Connect the Arduino to your network using an Ethernet shield.
- Upload the code to the Arduino using the Arduino IDE.
- Monitor the Serial Output to observe request counts and alerts.
- Adjust the Base Threshold as needed depending on expected network traffic.
## Future Enhancement

- Logging: Implement detailed logging for each request for further analysis.
- Web Interface: Create a simple web interface to monitor and manage the system remotely.
- Advanced Blocking: Use more sophisticated techniques for identifying malicious IPs.
## License

[MIT](https://choosealicense.com/licenses/mit/)

