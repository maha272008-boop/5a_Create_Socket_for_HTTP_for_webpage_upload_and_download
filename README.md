# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 

## server side:
```
import socket

s = socket.socket()
s.connect(("localhost",3024))

ch = input("1.Download 2.Upload : ")

if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())


s.close()

```

## client side:
```
import socket

s = socket.socket()
s.bind(("localhost",3024))
s.listen(1)

print("Server running...")

while True:
   c,addr = s.accept()
   
   request = c.recv(1024).decode()
   print("Request received")

   if "GET" in request:
       f = open("index.html","r")
       data = f.read()
       f.close()

       response = "HTTP/1.1 200 OK\n\n" + data
       c.send(response.encode())

   elif "POST" in request:
       data = request.split("\n\n")[1]

       f = open("upload.txt","w")
       f.write(data)
       f.close()

       c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())
c.close()

```
## Index html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <p>hello world</p>
</body>
</html>

```
## OUTPUT

<img width="1216" height="445" alt="{00C50FD0-1A7A-401F-99B4-DAB962170E20}" src="https://github.com/user-attachments/assets/4f46a8b3-dac1-4833-9f7b-f605bea42e05" />
<img width="1370" height="328" alt="{F8E0108B-DC8B-4262-A4A1-37E1CB39AAB2}" src="https://github.com/user-attachments/assets/c7c579d2-a6f5-4b21-9101-1ba3b1bc0a3a" />



## Result
Thus the socket for HTTP for web page upload and download created and Executed
