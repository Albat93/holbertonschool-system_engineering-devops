# 1. Distributed Web Infrastructure

This document illustrates a more fault-tolerant and scalable infrastructure for hosting `www.foobar.com`.

---

## 🔧 Diagram

```mermaid
graph TD
    User[User]
    DNS[DNS]
    LB[HAProxy Load Balancer]
    Server1[Server 1]
    Server2[Server 2]
    Nginx1[Nginx]
    Nginx2[Nginx]
    App1[App Server]
    App2[App Server]
    Code1[App Code]
    Code2[App Code]
    DB1[MySQL Primary]
    DB2[MySQL Replica]

    User --> DNS --> LB
    LB --> Server1
    LB --> Server2
    Server1 --> Nginx1 --> App1 --> Code1
    Server2 --> Nginx2 --> App2 --> Code2
    App1 --> DB1
    App2 --> DB2
    DB1 <---> DB2
```

---

## 💡 Explanation

### Why Add These Components?
- **HAProxy Load Balancer**: Distributes traffic to avoid overloading.
- **Two Servers**: High availability and redundancy.
- **Primary-Replica DB**: Improves read performance and fault tolerance.

### Load Balancer Algorithm
**Round Robin**: Alternates requests between servers.

### Active-Active vs Active-Passive
This setup is **Active-Active**, both servers serve traffic simultaneously.

### DB Replication
- **Primary**: Handles read and write.
- **Replica**: Read-only, replicates from primary.

---

## 🚨 Issues

- **SPOF**: Single Load Balancer
- **Security**: No firewall or HTTPS
- **No Monitoring**: No logs, alerts or performance metrics