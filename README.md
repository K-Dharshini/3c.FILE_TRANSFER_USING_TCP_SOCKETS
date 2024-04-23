# EXP7. CREATION FOR FILE TRANSFER USING TCP SOCKETS

## AIM:
To write a python program for creating File Transfer using TCP Sockets Links.

## ALGORITHM:
1. Import the necessary python modules.
   
2. Create a socket connection using socket module.
   
3. Send the message to write into the file to the client file.
   
4. Open the file and then send it to the client in byte format.
   
5. In the client side receive the file from server and then write the content into it.
   
## PROGRAM:
# CLIENT
~~~
import socket
s=socket.socket()
host=socket.gethostname()
port=60000
s.connect((host,port))
s.send("Hello server!".encode())
with open('received_file','wb') as f:
    while True:
        print('receiving data...')
        data=s.recv(1024)
        print('data=%s',(data))
        if not data:
            break
        f.write(data)
f.close()
print('Successfully get the file')
s.close()
print('connection closed')
~~~

# SERVER
~~~
import socket
port=60000
s=socket.socket()
host=socket.gethostname()
s.bind((host,port))
s.listen(5)
while True:
    conn,addr=s.accept()
    data=conn.recv(1024)
    print('Server received',repr(data))
    filename='mytext.txt'
    f=open(filename,'rb')
    l=f.read(1024)
    while(l):
        conn.send(l)
        print('Sent',repr(l))
        l=f.read(1024)
    f.close()
    print('Done sending')
    conn.send('Thank you for connecting'.encode())
    conn.close()
~~~

## OUTPUT:
# CLIENT
![image](https://github.com/K-Dharshini/3c.FILE_TRANSFER_USING_TCP_SOCKETS/assets/139334830/3f09ce8e-2a0a-4945-9872-1dd5051ee311)

# SERVER
![image](https://github.com/K-Dharshini/3c.FILE_TRANSFER_USING_TCP_SOCKETS/assets/139334830/abad2069-97dd-4ea6-9387-39e85fc3ac61)

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was successfully created and executed.
