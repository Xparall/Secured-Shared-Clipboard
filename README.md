# Secure Shared Clipboard with P2P and Web UI

## Overview
This project implements a **peer-to-peer (P2P) secured shared clipboard** where one device acts as a host, and other devices can join using a **Room ID & Password**. Clipboard data is synchronized in real-time across connected devices without a centralized server.

## Features
✅ **Peer-to-Peer Communication**: No centralized server required  
✅ **Basic Authentication**: Users join rooms with a **Room ID & Password**  
✅ **End-to-End Encryption**: AES-256 encryption for clipboard data  
✅ **Clipboard API Access**: Reads and writes clipboard across devices  
✅ **Auto Host Election**: If the host disconnects, another peer becomes the new host  
✅ **Web UI**: Control and manage clipboard sync through a browser  
✅ **Cross-Platform Support**: Works on **Windows, macOS, Linux, and Android**  

## Tech Stack
- **Backend**: C++ (with Boost.Asio / ZeroMQ for P2P communication)
- **Frontend**: Web UI (HTML, JavaScript, WebSockets)
- **Security**: AES-256 encryption for clipboard data
- **Authentication**: Basic authentication (username/password)
- **Clipboard Access**: Platform-specific APIs

## Architecture
1. **Host Device (Acts as a Server)**
   - Creates a **Room ID & Password**.
   - Runs a **local web server** for the Web UI.
   - Listens for **peer connections** and syncs clipboard changes.
   - Encrypts and shares clipboard updates with connected peers.

2. **Peer Devices (Join a Room)**
   - Open the Web UI → Enter **Room ID & Password**.
   - Connects to the host using **P2P WebSockets**.
   - Shares clipboard updates bi-directionally.

3. **Clipboard Sync**
   - When clipboard data changes, the host:
     - Encrypts the data (AES-256).
     - Sends it to connected peers.
   - Peers **decrypt & update** their clipboard.

4. **Auto Host Transfer**
   - If the host **disconnects**, another peer **becomes the new host** automatically.
   - Uses a **leader election algorithm** to determine the new host.

## API Endpoints
### **Authentication**
- `POST /auth/login` → Authenticate using Room ID & Password
- `GET /auth/logout` → Leave the room

### **Clipboard Operations**
- `POST /clipboard` → Copy text to clipboard (encrypted storage)
- `GET /clipboard` → Paste text from clipboard (with access control)

### **WebSockets for Real-Time Sync**
- `/ws/clipboard` → Real-time clipboard updates using WebSockets

## Installation & Setup
### **1. Clone the repository**
```sh
 git clone https://github.com/your-repo/secure-clipboard.git
 cd secure-clipboard
```

### **2. Setup Backend**
#### Install dependencies:
```sh
sudo apt install libboost-all-dev
sudo apt install libssl-dev
```

#### Build & Run the backend:
```sh
mkdir build && cd build
cmake ..
make
./secure_clipboard
```

### **3. Setup Frontend**
#### Run the frontend (Web UI):
```sh
cd frontend
python3 -m http.server 8080
```

## Security Measures
- **AES-256 encryption** for clipboard data before transmission.
- **Basic authentication** with Room ID & Password.
- **Auto host election** ensures clipboard sync continues even if the host leaves.

## Future Enhancements
- **File copy-paste support**
- **Mobile app integration**
- **Multi-room support**

## License
This project is licensed under the MIT License.

---

**Contributors**: 
- Yogesh J (@yogesh-goa)

For questions, reach out at **yogesh.hedode@gmail.com**.
