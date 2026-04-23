# System Design: Multi-User Chat Application

## Overview
Real-time chat system supporting multiple concurrent users with WebSocket communication.

## Architecture

### Components
- **Client**: Vue.js frontend with Socket.IO client
- **Server**: Node.js backend with Socket.IO server
- **Database**: PostgreSQL for message persistence
- **Proxy**: Nginx for routing and SSL termination

### Technology Stack
- Frontend: Vue.js 3 + Socket.IO-client
- Backend: Node.js + Express + Socket.IO
- Database: PostgreSQL
- Deployment: Docker Compose

## Data Flow

```mermaid
sequenceDiagram
    participant C1 as Client 1
    participant S as Server
    participant C2 as Client 2
    participant DB as PostgreSQL

    C1->>S: WebSocket Connect
    S->>DB: Store connection
    S-->>C1: Connected
    C2->>S: WebSocket Connect
    S->>DB: Store connection
    S-->>C2: Connected
    C1->>S: Send Message
    S->>DB: Save message
    S->>C1: Broadcast
    S->>C2: Broadcast