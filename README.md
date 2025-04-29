# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
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
```python
import socket
c = socket.socket()
c.connect(('localhost', 9999))
size = int(input("Enter number of frames to send: "))
l = list(range(size))  
print("Total frames to send:", len(l))
s = int(input("Enter Window Size: "))
i = 0
while True:
    while i < len(l):
        st = i + s
        frames_to_send = l[i:st]  
        print(f"Sending frames: {frames_to_send}")
        c.send(str(frames_to_send).encode())  
        ack = c.recv(1024).decode()  
        if ack:
            print(f"Acknowledgment received: {ack}")
            i += s  
    break
c.close()  
```
SERVER:
```python
import socket
s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server listening...")
conn, addr = s.accept()
print(f"Connected to {addr}")
while True:
    frames = conn.recv(1024).decode()
    if not frames:
        break
    print(f"Received frames: {frames}")
    ack_message = f"ACK for frames: {frames}"
    conn.send(ack_message.encode())
conn.close()  
s.close()  
```
## OUTPUT
CLIENT:

![Screenshot 2025-04-29 200639](https://github.com/user-attachments/assets/3887fdb5-c266-45ba-824b-9463f27c4bd5)

SERVER:

![image](https://github.com/user-attachments/assets/4bcc238f-05d9-45f3-bf1b-e01f44241b66)

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
