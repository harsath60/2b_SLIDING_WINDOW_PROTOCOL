# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## Developed By: Harsath S
## Reg No: 212225230096

## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
### Server.py
```py
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)

print("Server waiting for client...")
c, addr = s.accept()

size = int(input("Enter number of frames to send: "))
l = list(range(size))

ws = int(input("Enter Window Size: "))

st = 0
i = 0

while i < len(l):
    st = i + ws

    print("Sending frames:", l[i:st])
    c.send(str(l[i:st]).encode())

    ack = c.recv(1024).decode()

    if ack:
        print(ack)
        i += ws
    else:
        break

c.close()
s.close()
```
### Client.py
```py
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    data = s.recv(1024).decode()

    if data:
        print("Received frames:", data)

        s.send("ACK: Frames received".encode())
    else:
        break

s.close()
```
## OUPUT

<img width="1917" height="1015" alt="Screenshot 2026-11-25 101255" src="https://github.com/user-attachments/assets/034ecfb9-8e9e-42cc-9415-7daa08076417" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
