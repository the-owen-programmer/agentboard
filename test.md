# Rec Room Android API Reference

**Version:** March 2026  
**Platform:** Android APK  
**Decompilation Date:** October 13, 2026  
**Total API Endpoints:** 504  

## Table of Contents

1. [Overview](#overview)
2. [Network Architecture](#network-architecture)
3. [API Endpoint Categories](#api-endpoint-categories)
4. [Service Client Classes](#service-client-classes)
5. [Data Models](#data-models)
6. [Network Protocols](#network-protocols)
7. [Authentication](#authentication)
8. [Example Usage](#example-usage)

---

## Overview

The Rec Room Android game uses a RESTful API architecture combined with real-time Photon networking for multiplayer functionality. The API is organized into multiple modules covering player accounts, rooms, economy, matchmaking, social features, and game-specific services.

### Architecture Components

- **REST API Layer**: Handles all HTTP-based requests
- **Photon Networking**: Real-time multiplayer communication
- **Protobuf Serialization**: Binary data serialization
- **Service Clients**: Wrapper classes for API interactions
- **Data Models**: Request/response DTOs for all API calls

---

## Network Architecture

### HTTP Client Infrastructure

```
Application Layer
    ↓
Service Client Classes
    ↓
HTTP Client (GVMCHNLYPGE / System.Net.Http)
    ↓
SSL/TLS Encrypted Transport
    ↓
Rec Room API Servers
```

### Key Networking Components

| Component | File | Purpose |
|-----------|------|---------|
| `RRNetworkLayer` | RecRoom.Networking.RRNetworkLayer.dll.cs | Core networking behavior and state management |
| `PhotonImpl` | RecRoom.Networking.PhotonImpl.Runtime.dll.cs | Photon real-time networking implementation |
| `GVMCHNLYPGE` | RecNet.Utilities.dll.cs | HTTP client wrapper |
| `RRHttpClient` | RecRoom.Networking.dll.cs | Custom HTTP client with session management |

### Socket and Transport

- TCP sockets with binary protocol
- WebSocket support for real-time features
- Connection pooling for optimized performance
- Automatic retry with exponential backoff

---

## API Endpoint Categories

### 1. Account Management

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/account/me` | GET/PUT | Current user information |
| `/account/me/changepassword` | POST | Change password |
| `/account/me/createlogintoken` | POST | Create login token |
| `/account/me/haspassword` | GET | Check if password exists |
| `/account/me/remoteauth` | POST | Remote authentication |
| `/account/recoverpassword` | POST | Password recovery |
| `/account/search` | POST | Search accounts |

### 2. Room Management

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/room/` | POST | Create room |
| `/room/{0}` | GET/PUT/DELETE | Room details |
| `/room/{0}/instances` | GET | Get room instances |
| `/rooms/search` | POST | Search rooms |
| `/rooms/bulk` | POST | Bulk room operations |
| `/rooms/{0}/assets` | GET | Room assets |
| `/rooms/{0}/permissions` | GET/PUT | Room permissions |
| `/rooms/{0}/bans` | POST | Ban/unban players |
| `/rooms/{0}/members` | POST | Room members management |