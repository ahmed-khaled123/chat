# 🗨️ Assignment 04 — Go RPC Chatroom

This project demonstrates a **simple chatroom system** built using Go’s `net/rpc` package.  
It allows multiple clients to connect to a central server, send messages, and receive the entire chat history in real-time.

---

## 🎥 Demo Video
[Deployment Video (Google Drive)](https://drive.google.com/file/d/1w063q1xQaT_qlnvpiE8zTZQWMPEEAjej/view?usp=sharing)

---

## 🚀 Overview

- The **server** acts as the main message coordinator.  
- The **clients** connect to it using RPC, send chat messages, and retrieve the complete history after every message.

The chat continues until the user types `exit` or closes the terminal.

---

## ⚙️ Features

- 💬 **Persistent chat history (in-memory)** — the server keeps all previous messages.  
- 🔄 **Real-time updates** — every message returns the full chat log to all users.  
- 👥 **Multiple clients** — connect several clients to the same server.  
- 🧵 **Thread-safe operations** — concurrency handled using a mutex.  
- 🧹 **Graceful exit** — typing `exit` ends the client session cleanly.  

---

## 📁 Project Structure

### **server.go**
- Implements the `ChatServer` RPC service.  
- Exposes two main methods:
  - `SendMessage(ChatMessage)` → appends a new message and returns the updated chat history.  
  - `GetHistory()` → retrieves all stored messages.  
- Uses a **mutex** to ensure thread-safe access to shared memory.

### **client.go**
- Asks for a **username** at startup.  
- Reads full lines (supports spaces) using `bufio.Reader`.  
- Sends messages to the server via RPC and displays the entire chat history after each send.  
- Detects connection issues and exits gracefully.

---

## 🧩 How to Run

1️⃣ **Start the server**
```bash
go run server.go
```

2️⃣ **Launch one or more clients** (each in a new terminal)
```bash
go run client.go
```

3️⃣ **Sample Output**
```
--- Chat History ---
Alice: Hi everyone!
Bob: Hey Alice, how are you?
---------------------
```

---

## 🧠 Notes

- Works with **Go 1.20+**
- The project doesn’t require any external dependencies.
- Data is stored in memory only (no database involved).
