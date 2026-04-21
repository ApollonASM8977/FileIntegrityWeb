# ðŸ›¡ï¸ FileIntegrityWeb

> Cryptographic file hashing & integrity verification â€” built with FastAPI and a React cyberpunk UI.

![Python](https://img.shields.io/badge/Python-3.11+-blue?logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/Backend-FastAPI-009688?logo=fastapi)
![React](https://img.shields.io/badge/Frontend-React%2018-61DAFB?logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript)
![License](https://img.shields.io/badge/License-Proprietary-red)
![Security](https://img.shields.io/badge/Crypto-SHA256%20%2B%20HMAC-green)

---

## What is FileIntegrityWeb?

FileIntegrityWeb is a full-stack web application that lets you **hash any file with a cryptographic algorithm** and later **verify that the file hasn't been tampered with**.  
Every hash is protected by an HMAC signature â€” ensuring both integrity and authenticity.

---

## Features

| Feature | Details |
|---|---|
| ðŸ”¢ Multi-Algorithm Hashing | SHA-256, SHA-512, SHA-1, MD5 â€” your choice |
| ðŸ” HMAC Protection | HMAC-SHA256 signature on every stored hash |
| âœ… Integrity Verification | Re-upload any file to instantly check if it changed |
| ðŸ“‹ Hash History | Browse all stored records with full hash & HMAC values |
| â¬‡ï¸ Hash Download | Export any `.hash` file for offline archiving |
| ðŸ—‘ï¸ Record Management | Delete individual entries or clear all at once |
| ðŸŽ¨ Cyberpunk UI | Dark terminal-style interface with glowing green accents |

---

## Security Model

```
File â”€â”€â–º hashlib (SHA-256 / SHA-512 / SHA-1 / MD5) â”€â”€â–º hash_value
  â”‚
  â””â”€â”€â–º HMAC-SHA256 (server secret key) â”€â”€â–º hmac_value
                                               â”‚
                              stored together in hash_storage/
```

- **HMAC protects against hash file tampering** â€” even if the `.hash` file is modified, HMAC verification will fail
- **Secret key** loaded from `HMAC_SECRET` env variable (random on each restart if not set)
- **Constant-time comparison** via `hmac.compare_digest` â€” no timing attacks
- **Filename sanitization** â€” `Path(filename).name` strips any path traversal

---

## Installation

```bash
# Clone the repository
git clone https://github.com/ApollonASM8977/FileIntegrityWeb.git
cd FileIntegrityWeb
```

### Backend (FastAPI)

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
# API running at http://localhost:8000
```

### Frontend (React + Vite)

```bash
cd frontend
npm install
npm run dev
# App running at http://localhost:5173
```

> The Vite dev server proxies `/api/*` â†’ `http://localhost:8000` automatically.

---

## Project Structure

```
FileIntegrityWeb/
â”œâ”€â”€ backend/
â”‚   â”œâ”€â”€ main.py              # FastAPI app â€” all routes & crypto logic
â”‚   â”œâ”€â”€ requirements.txt
â”‚   â”œâ”€â”€ .env.example         # HMAC_SECRET env variable template
â”‚   â”œâ”€â”€ uploads/             # Uploaded files (gitignored)
â”‚   â””â”€â”€ hash_storage/        # Stored .hash files (gitignored)
â”‚
â””â”€â”€ frontend/
    â”œâ”€â”€ src/
    â”‚   â”œâ”€â”€ App.tsx                    # Main shell â€” tab navigation
    â”‚   â”œâ”€â”€ components/
    â”‚   â”‚   â”œâ”€â”€ UploadTab.tsx          # Upload & hash a file
    â”‚   â”‚   â”œâ”€â”€ VerifyTab.tsx          # Verify file integrity
    â”‚   â”‚   â”œâ”€â”€ HistoryTab.tsx         # Browse stored records
    â”‚   â”‚   â”œâ”€â”€ AlgoSelector.tsx       # Algorithm picker
    â”‚   â”‚   â””â”€â”€ DropZone.tsx           # Drag & drop file input
    â”‚   â””â”€â”€ index.css                  # Global styles + cyberpunk theme
    â”œâ”€â”€ tailwind.config.js
    â””â”€â”€ vite.config.ts
```

---

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/` | Health check |
| `GET` | `/algorithms` | List available algorithms |
| `POST` | `/upload` | Upload file â†’ returns hash + HMAC |
| `POST` | `/verify` | Verify file against stored hash |
| `GET` | `/files` | List all stored records |
| `GET` | `/download/{filename}/{algo}` | Download a `.hash` file |
| `DELETE` | `/files` | Delete all files and hashes |
| `DELETE` | `/files/{filename}/{algo}` | Delete a specific record |

---

## Usage

1. **Upload** â€” drop a file, pick an algorithm, click *Upload & Hash*
2. **Store** â€” copy the hash or download the `.hash` file for reference
3. **Verify** â€” later, drop the same file in the *Verify* tab
4. **Result** â€” instant verdict: âœ… *INTEGRITY VERIFIED* or âŒ *INTEGRITY FAILURE*
5. **History** â€” manage all your records from the *History* tab

---

## Tech Stack

- **Backend** â€” FastAPI, Python 3.11, Uvicorn
- **Hashing** â€” hashlib (SHA-256, SHA-512, SHA-1, MD5)
- **HMAC** â€” Python `hmac` module (HMAC-SHA256)
- **Frontend** â€” React 18, TypeScript, Vite
- **Styling** â€” Tailwind CSS (custom cyberpunk palette)
- **HTTP Client** â€” Axios

---

## Author

**Aboubacar Sidick Meite** â€” Cybersecurity Student  
[GitHub](https://github.com/ApollonASM8977)

---

## License

Â© 2026 Aboubacar Sidick Meite â€” All Rights Reserved.  
Unauthorized copying, distribution or modification is strictly prohibited.

