Here’s a simple Python implementation of a TCP Echo Client-Server. The server will echo back whatever message it receives from the client.

### **TCP Echo Server**

```python
import socket

def tcp_echo_server(host='127.0.0.1', port=12345):
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as server_socket:
        server_socket.bind((host, port))
        server_socket.listen(1)
        print(f"Server listening on {host}:{port}")

        while True:
            conn, addr = server_socket.accept()
            with conn:
                print(f"Connected by {addr}")
                while True:
                    data = conn.recv(1024)
                    if not data:
                        break
                    print(f"Received from client: {data.decode()}")
                    conn.sendall(data)

if __name__ == "__main__":
    tcp_echo_server()
```

---

### **TCP Echo Client**

```python
import socket

def tcp_echo_client(host='127.0.0.1', port=12345):
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as client_socket:
        client_socket.connect((host, port))
        print(f"Connected to server at {host}:{port}")

        while True:
            message = input("Enter message to send (or 'exit' to quit): ")
            if message.lower() == 'exit':
                print("Closing connection.")
                break

            client_socket.sendall(message.encode())
            data = client_socket.recv(1024)
            print(f"Received from server: {data.decode()}")

if __name__ == "__main__":
    tcp_echo_client()
```

---

### **How It Works**
1. **Server**:
   - Binds to a specified IP address and port.
   - Listens for incoming connections.
   - Echoes back any data received from the client.
   
2. **Client**:
   - Connects to the server at the specified IP and port.
   - Sends user-inputted messages to the server.
   - Displays the server's response.

---

### **Usage**
1. Run the server program first:
   ```bash
   python server.py
   ```
2. In a separate terminal, run the client program:
   ```bash
   python client.py
   ```
3. Enter messages in the client terminal. The server will echo them back.

---

### **Example Interaction**
**Client:**
```
Enter message to send (or 'exit' to quit): Hello, Server!
Received from server: Hello, Server!
Enter message to send (or 'exit' to quit): exit
Closing connection.
```

**Server:**
```
Server listening on 127.0.0.1:12345
Connected by ('127.0.0.1', 54321)
Received from client: Hello, Server!
```
