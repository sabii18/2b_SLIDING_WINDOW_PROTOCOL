# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM:
To implement the program for Sliding Window Protocol
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
### Server:
~~~
import socket

s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)

c, addr = s.accept()
while True:
    data = c.recv(1024).decode()
    if not data:
        break

    print("Received:", data)
    c.send(f"ACK: {data}".encode())

c.close()
s.close()
~~~
### Client:
~~~
import socket

c = socket.socket()
c.connect(('localhost', 9999))

n = int(input("No. of frames: "))
w = int(input("Window size: "))
frames = list(range(n))

i = 0
while i < n:
    send = frames[i:i+w]
    print("Sending:", send)
    c.send(str(send).encode())

    ack = c.recv(1024).decode()
    print(ack)
    print()
    i += w

c.close() 
~~~
## OUPUT
### Server:
<img width="767" height="306" alt="image" src="https://github.com/user-attachments/assets/3ff6a3d5-78b8-4d72-95ef-e0a3a7085b83" />

### Client:
<img width="766" height="422" alt="image" src="https://github.com/user-attachments/assets/b592ac14-19ef-4509-9edb-aee4c7ed5453" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
