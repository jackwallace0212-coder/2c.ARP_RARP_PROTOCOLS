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
```
server

import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")

c, addr = s.accept()
print(f"Connection established with {addr}")

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()

    if not ip:  
        break

    try:
        mac = address[ip]  # Get the MAC address for the IP
        print(f"IP: {ip} -> MAC: {mac}")
        c.send(mac.encode())  
    except KeyError:
        print(f"IP: {ip} not found in ARP table.")
        c.send("Not Found".encode())
c.close()
s.close()
client

import socket
c = socket.socket()
c.connect(('localhost', 8000))

while True:
    ip = input("Enter IP address to find MAC (or type 'exit' to quit): ")

    if ip.lower() == "exit":  
        break

    c.send(ip.encode())
    mac = c.recv(1024).decode()
    print(f"MAC Address for {ip}: {mac}")
c.close()
```
## OUPUT - ARP

<img width="1025" height="86" alt="562044493-8729fd43-b242-4f37-95f5-34b29ef6d115" src="https://github.com/user-attachments/assets/55cdac37-731b-464a-8c79-25a234afb571" />
<img width="941" height="90" alt="562044557-14d38a99-225e-49de-bf3e-58b24626d8c4" src="https://github.com/user-attachments/assets/74e355cc-3f0e-4062-9d41-4b18cf0c99cc" />

## PROGRAM - RARP
```
server

import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening for RARP requests...")
c, addr = s.accept()
print(f"Connection established with {addr}")

rarp_table = {
    "6A:08:AA:C2": "165.165.80.80",
    "8A:BC:E3:FA": "165.165.79.1"
}

while True:
    mac = c.recv(1024).decode()

    if not mac:  
        break

    try:
        ip = rarp_table[mac]  
        print(f"MAC: {mac} -> IP: {ip}")
        c.send(ip.encode())  
    except KeyError:
        print(f"MAC: {mac} not found in RARP table.")
        c.send("Not Found".encode())
c.close()
s.close()

client

import socket
c = socket.socket()
c.connect(('localhost', 8000))

while True:
    mac = input("Enter MAC address to find IP (or type 'exit' to quit): ")
    if mac.lower() == "exit":  
        break
    c.send(mac.encode())
    ip = c.recv(1024).decode()
    print(f"IP Address for {mac}: {ip}")
c.close()
```
## OUPUT -RARP
<img width="983" height="90" alt="562044313-7c423e56-3420-4d84-9262-19255a5a7c80" src="https://github.com/user-attachments/assets/71708100-43da-4c93-80a9-03397114aea8" />
<img width="1030" height="85" alt="562044364-03215a39-4164-4757-8bf1-f31232bcf6ab" src="https://github.com/user-attachments/assets/26fe45c1-b534-4aa8-af32-9b11d1738d41" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
