# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
## arp_server.py
```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)

print("ARP Server is listening on port 8000...")
c, addr = s.accept()
print("Connected with", addr)

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()

    if not ip or ip.lower() == 'exit':
        print("Client disconnected.")
        break

    print("Received IP:", ip)
    mac = address.get(ip, "Not Found")
    c.send(mac.encode())

c.close()
s.close()
```
## arp_client.py
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter Logical Address (IP) (or 'exit'): ")

    if ip.lower() == 'exit':
        s.send(ip.encode())
        break

    s.send(ip.encode())
    mac = s.recv(1024).decode()
    print("MAC Address:", mac)

s.close()
```
## OUPUT - ARP
<img width="1049" height="190" alt="Screenshot 2026-03-25 103312" src="https://github.com/user-attachments/assets/adda4e38-1d46-4511-90f8-15239586cf02" />

## PROGRAM - RARP
## rarp_server.py
```
import socket

s = socket.socket()
s.bind(('localhost', 8001))
s.listen(1)

print("RARP Server is listening on port 8001...")
c, addr = s.accept()
print("Connected with", addr)

address = {
    "6A:08:AA:C2": "165.165.80.80",
    "8A:BC:E3:FA": "165.165.79.1"
}

while True:
    mac = c.recv(1024).decode()

    if not mac or mac.lower() == 'exit':
        print("Client disconnected.")
        break

    print("Received MAC:", mac)
    ip = address.get(mac, "Not Found")
    c.send(ip.encode())

c.close()
s.close()
```
## rarp_client.py
```
import socket

s = socket.socket()
s.connect(('localhost', 8001))

while True:
    mac = input("Enter Physical Address (MAC) (or 'exit'): ")

    if mac.lower() == 'exit':
        s.send(mac.encode())
        break

    s.send(mac.encode())
    ip = s.recv(1024).decode()
    print("IP Address:", ip)

s.close()
```
## OUPUT -RARP
<img width="1051" height="194" alt="Screenshot 2026-03-25 103434" src="https://github.com/user-attachments/assets/58011403-5564-4771-9f13-3a089f4b5ea8" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
