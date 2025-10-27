# Net-Abdel-Network-Scanner
A simple network scanner to detect devices, open ports, and services in a local network.  
Built for learning networking and cybersecurity fundamentals.

## Features
- Discover active hosts in the network
- Scan open ports
- Identify basic services running on devices
- Generate a simple report

## Tools & Technologies
- Python 3
- Socket programming
- subprocess (for ping)
- Optional: Nmap library for advanced scanning
- NetAbdel-Network-Scanner/
├── scanner.py       # Main Python script
├── README.md        # Project description
├── requirements.txt # Dependencies (if any)
└── sample_report.txt # Example output
import subprocess
import socket

def ping_host(ip):
    try:
        subprocess.check_output(["ping", "-c", "1", ip])
        return True
    except subprocess.CalledProcessError:
        return False

def scan_ports(ip, ports=[22, 80, 443]):
    open_ports = []
    for port in ports:
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(0.5)
        result = sock.connect_ex((ip, port))
        if result == 0:
            open_ports.append(port)
        sock.close()
    return open_ports

if __name__ == "__main__":
    network_prefix = "192.168.1."
    for i in range(1, 20):
        ip = network_prefix + str(i)
        if ping_host(ip):
            print(f"Host {ip} is active.")
            ports = scan_ports(ip)
            if ports:
                print(f"  Open ports: {ports}")
            else:
                print("  No common ports open.")

              
