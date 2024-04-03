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
## PROGRAM - ARP:
```
import socket

def arp_client(ip_address):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect(('localhost', 12345))
    s.send(ip_address.encode())
    mac_address = s.recv(1024).decode()
    print(f"MAC Address for IP {ip_address}: {mac_address}")
    s.close()

if __name__ == "__main__":
    ip_address = input("Enter the IP address to resolve: ")
    arp_client(ip_address)


```
## OUTPUT - ARP
 ![image](https://github.com/vamsikrishna272005/2c.ARP_RARP_PROTOCOLS/assets/147477015/809371d3-bdde-45a7-91c4-74ca6eeba446)

## PROGRAM - RARP:
```
import socket

def arp_server():
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.bind(('localhost', 12345))
    s.listen(5)
    print("ARP Server started...")
    while True:
        client_socket, addr = s.accept()
        ip_address = client_socket.recv(1024).decode()
        mac_address = get_mac_address(ip_address)
        client_socket.send(mac_address.encode())
        client_socket.close()

def get_mac_address(ip_address):
    # Simulated MAC address lookup table
    mac_address_table = {
        '192.168.1.1': '00:11:22:33:44:55',
        '192.168.1.2': 'AA:BB:CC:DD:EE:FF',
        '192.168.1.3': '12:34:56:78:90:AB'
    }
    return mac_address_table.get(ip_address, "MAC Address not found")

if __name__ == "__main__":
    arp_server()

```
### OUTPUT - RARP
![image](https://github.com/vamsikrishna272005/2c.ARP_RARP_PROTOCOLS/assets/147477015/6c2dada9-5ab6-4253-819a-a62109cdb645)


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully executed.
