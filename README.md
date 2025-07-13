# 🧩 Chat Service
![Go Version](https://img.shields.io/badge/go-1.20+-blue)
![License](https://img.shields.io/badge/license-private-lightgrey)
![Status](https://img.shields.io/badge/status-active-brightgreen)

## 📝 Description

This repository contains a **Chat Message Service** built in Go. It handles real-time messaging between clients and customer service agents using WebSocket, Redis, and MongoDB. The system is optimized for scalability and maintainability, supporting one-to-many communication and multi-session handling.

---

## 🚀 Features

- ✅ Real-time chat using WebSocket
- ✅ One-to-many communication (1 client → many agents)
- ✅ Typing indicator & read/unread status
- ✅ Reply to specific message (thread-style)
- ✅ Upload & send media (image, video, voice, document)
- ✅ Temporary file handling and AWS S3 integration
- ✅ Grouping and filtering clients (admin side)
- ✅ IndexedDB support for offline history (client side)
- ✅ Admin dashboard with:
  - Client list view
  - Unread message count
  - Message search by keyword
  - Drag-and-drop media upload

---

## 📦 Modules & Layers

- **WebSocket Layer:** Manages real-time messaging, typing, and status updates.
- **Message Handler:** Processes all incoming messages and triggers appropriate logic (e.g. store, broadcast, upload).
- **Redis Pub/Sub:** Distributes messages across instances (horizontal scaling).
- **MongoDB:** Stores chat messages, user data, and media metadata.
- **S3 Integration:** Uploads and retrieves media files (images, videos, recordings).
- **Admin API:** Backend services for chat admin dashboard.
- **Middleware:** Handles auth, logging, and request pre/post-processing.
- **File Processor:** Manages temporary image storage and background upload.
- **Logger:** Outputs system logs to a file with rotation support.

---

## 📁 Directory Structure

```
chat-service
    L external                       → Contains for calling other services or connections
    L handler                        → Manages control logic for handling HTTP requests
    L helper                         → Stores common functions the application
    L images                         → Directory for save image temporary
    L initializer                    → Contains for initialize database, websocket, redis and another connection
    L logs                           → The directory to save log file
    L middleware                     → Contains middleware for processing requests/responses before or after reaching the controller
    L migrations                     → Contains migration database
    L models                         → Object models representing the application's or database's data structure
    L ws                             → Stores the application's core business logic on websocket
```
## How to setup

```
- Clone this repository
- go mod tidy
- copy .env.example to .env (if you want to run with consul)
- copy .config.json.example to .config.json
```

## How to Migration

```bash
go run ./migration/fresh/main.go (only for truncate or create data master)
go run ./migration/update/main.go (only for update and create new table and column)
```
## How to run

```bash
go mod tidy
go run main.go
```

## How to run with docker

```bash
docker-compose up -d --build --force-recreate
```

## How to build
```bash
make build
```
