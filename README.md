# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM:
To write a python program to perform sliding window protocol
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
CLIENT:

```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Waiting for a connection...")
c, addr = s.accept()
print("Connected to:", addr)
size = int(input("Enter number of frames to send: "))
frames = list(range(size))  
window_size = int(input("Enter Window Size: "))
i = 0  
while i < len(frames):
    send_frames = frames[i : i + window_size]
    c.send(str(send_frames).encode())  
    print(f"Sent: {send_frames}")
    ack = c.recv(1024).decode()
    if ack:
        print(f"Acknowledgment received: {ack}")
    i += window_size  
print("All frames sent. Closing connection.")
c.close()
s.close()
```

SERVER:
```import socket
s = socket.socket()
s.connect(('localhost', 8000))
while True:
   data = s.recv(1024).decode() 
    if not data:
        break  
    print("Received:", data)  
    s.send("Acknowledgement received from the client".encode())
s.close()
```
## OUPUT

![Screenshot 2025-03-17 132719](https://github.com/user-attachments/assets/9620cdb5-ae8c-4ea0-be50-0866bbf0bee3)

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
