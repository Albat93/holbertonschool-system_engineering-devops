# 2. Secured and Monitored Web Infrastructure

This setup secures and monitors the web infrastructure for `www.foobar.com`.

---

## 🔐 Diagram

```mermaid
graph TD
    Internet[Internet]
    FW1[Firewall #1]
    LB1[HAProxy + SSL LB1]
    FW2[Firewall #2]
    FW3[Firewall #3]
    ServerA[Server A]
    ServerB[Server B]
    NginxA[Nginx]
    NginxB[Nginx]
    AppA[App Server]
    AppB[App Server]
    DB1[MySQL Primary]
    DB2[MySQL Replica]
    MonA[Monitoring Agent A]
    MonB[Monitoring Agent B]
    MonLB[Monitoring Agent LB]
    Sumo[Sumologic/Monitoring Platform]

    Internet --> FW1 --> LB1
    LB1 --> FW2 --> ServerA
    LB1 --> FW3 --> ServerB
    ServerA --> NginxA --> AppA --> DB1
    ServerB --> NginxB --> AppB --> DB2
    DB1 <--> DB2

    MonLB --> Sumo
    MonA --> Sumo
    MonB --> Sumo
```

---

## 🔍 Explanation

### Why Add These Components?

- **Firewalls**: Control traffic, protect against attacks.
- **HTTPS (SSL)**: Encrypts data to ensure security.
- **Monitoring Agents**: Track metrics and logs for health checks.

### Monitoring
- Uses agents (e.g., Sumologic) to send logs and metrics.
- For QPS monitoring: track HTTP logs or use tools like Prometheus.

---

## 🚨 Issues

- **SSL Termination at LB**: Internal traffic is unencrypted.
- **Single MySQL Writer**: Fails if primary goes down.
- **All-in-One Servers**: Risk of interdependent failures.
