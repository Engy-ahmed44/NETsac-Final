
# 📂 CipherShare: A Peer-to-Peer File Sharing System with Access Control and Encryption

## 🧩 Overview

CipherShare is a peer-to-peer (P2P) file sharing system implemented in Python. It allows users to:

* Register and log in securely
* Upload and download encrypted files
* Request access to files from peers
* Grant file access selectively
* Transfer files either through a central peer or directly (P2P)

All files are encrypted using AES-GCM for confidentiality, and access control is managed through a JSON-based system.

---

## 🚀 Features

* 🔒 AES-128 GCM file encryption/decryption
* 👤 User authentication with salted hashed passwords (PBKDF2-HMAC-SHA256)
* 📤 File upload/download with peer-to-peer fallback logic
* 🛡️ Access control via request/grant system
* 📡 Peer notifications and proxy handling
* 🧭 Interactive command-line client (REPL)

---

## 📦 Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/yourusername/CipherShare.git
   cd CipherShare/project
   ```

2. **Create a virtual environment (optional but recommended):**

   ```bash
   python -m venv venv
   source venv/bin/activate  # on Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**

   ```bash
   pip install cryptography 
   ```
   3.1. **If Gui is include, you'd need to install all the requirements**
   ```bash
   pip install requirments.txt
   ```

---

## 🛠️ Usage

### Start a peer node

Each peer needs to run their own instance with a specific port:

```bash
python index.py <port>
```

For example:

```bash
python index.py 3000
```

This starts:

* A **peer server** listening on the specified port
* An interactive **client console** (REPL)

### Example Workflow

1. **Connect to another peer:**

   ```
   p2p> connect localhost 3001
   ```

2. **Register or login:**

   ```
   p2p> register
   p2p> login
   ```

3. **Upload a file:**

   ```
   p2p> upload example.txt
   ```

4. **Request file from another peer:**

   ```
   p2p> request secret.jpg localhost 3001 alice
   ```

5. **Grant access to a file:**

   ```
   p2p> grant secret.jpg bob
   ```

6. **Download the granted file:**

   ```
   p2p> download secret.jpg
   ```

7. **View peer list and file status:**

   ```
   p2p> peerlist
   ```

---

## 🗂 File Structure

* `index.py` – Entry point that launches both peer and client.
* `fileshare_client.py` – Handles client-side interaction and commands.
* `fileshare_peer.py` – Server-side logic for managing users and file transfers.
* `crypto_utils.py` – Handles encryption, password hashing, and access control persistence.
* `access_requests.json` – Tracks requests, grants, and private files.
* `GLOBAL_KEY.bin` – Symmetric AES key (auto-generated on first run).
* `users.json` – Stores user credentials (hashed & salted).

---

## 🧪 Testing the System Locally

To simulate multiple peers:

1. Open two terminal windows.
2. In Terminal 1:

   ```bash
   python index.py 3000
   ```
3. In Terminal 2:

   ```bash
   python index.py 3001
   ```

Each one will act as an independent peer that can register, upload, and exchange files with the other.

---

## 🔐 Security Notes

* File encryption uses **AES-GCM (128-bit)** for confidentiality and integrity.
* Passwords are stored using **PBKDF2 with SHA-256 and random salt**.
* Files are decrypted only upon download on the client side.

---

## 📋 Command Summary

| Command    | Description                                              |
| ---------- | -------------------------------------------------------- |
| `connect`  | Connect to another peer (e.g., `connect 127.0.0.1 3001`) |
| `register` | Register a new user                                      |
| `login`    | Log in as a user                                         |
| `upload`   | Upload and encrypt a file                                |
| `list`     | List accessible files                                    |
| `download` | Download and decrypt a file                              |
| `request`  | Request access to another peer’s file                    |
| `grant`    | Grant access to a requested file                         |
| `peerlist` | View status of all files and access control              |
| `quit`     | Exit the CLI                                             |

---

## 🧠 Future Work

* 🌐 NAT traversal / external IP detection
* 💬 GUI interface for non-technical users
* 📜 Persistent logging of transfers and errors
* 🔑 Per-user symmetric keys instead of global key
* 🔁 Background sync/replication of granted files

