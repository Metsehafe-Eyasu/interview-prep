---
title: "Audit System for Trading Platform"
company: "Bloomberg"
category: "system-design"
role: "internship" 
date: "2024-01-08"
---

# Audit System for Trading Platform

## Context
We have an **existing trading system** with critical features:
1. **Track a stock’s price** (real-time updates).
2. **Buy a stock** from third-party APIs.
3. (Potentially one more feature—assume standard trading actions.)

Speed is **essential**, so the new component should not **significantly** slow down existing operations.

## Task
Design a **stand-alone audit service** that integrates with this trading system. The audit service must support:
1. **Find the history** of one user’s actions (a “search by user” feature).
2. **Generate a document** of a user’s historical actions (e.g., a PDF or downloadable report).
3. **Provide a live feed** of one user’s actions (real-time streaming or near-real-time updates).

## Requirements
1. **High Write Throughput**: The trading system may process high volumes of transactions.
2. **Fast Reads**: Must be able to query or stream user actions quickly without blocking critical trading flows.
3. **Stand-alone**: The audit service runs separately but has real-time or near-real-time data integration with the main trading system.
4. **Scalability**:
   - Should handle spikes in transaction volume (e.g., market open).
   - Support growing user base.
5. **Reliability / Durability**:
   - Audit logs must not be lost, even under failures.
   - Potential compliance or legal requirements for storing transaction history.

## Potential Approaches

### 1. **Data Ingestion & Storage**
- **Event-Driven**: The trading system publishes user actions (buy, price watch, etc.) as **events** to a message bus (e.g., Kafka, RabbitMQ).
- The **audit service** consumes these events and writes them to a dedicated audit database (e.g., **NoSQL** for high write throughput, or an **append-only** structured store).
- **Why Event-Driven?** Decouples the audit logic from the trading logic, ensuring minimal impact on the trading system’s speed.

### 2. **Database & Indexing**
- **Append-Only Log** or **Time-Series DB**: Each user action is written chronologically.
- **Search**: For quick queries by user ID, maintain an index keyed by `user_id`.
- **Generating Documents**: Possibly generate on-the-fly using a **reporting service** or store pre-aggregated data.
- **Real-Time Feed**: Use something like **WebSockets**, **long polling**, or **server-sent events** (SSE) to push new user actions as they happen.

### 3. **Architecture Diagram (High-Level)**
```
+-------------------+        +-------------------+
| Trading System    |        | Audit Service     |      +-------------------+
| (Existing)        |        | (New)             |      | Audit DB          |
|  - Buys Stock     | --->   |  - Consumes       | ---> | (NoSQL or RDBMS)  |
|  - Tracks Prices  | Kafka  |    user actions   |      +-------------------+
|  - Etc.           |        |  - Stores in DB   |
+-------------------+        +-------------------+
                                        |                          
                                        | (User requests history)  
                                        v                         
                                    +-------------------+     
                                    |  UI / Client App  |     
                                    +-------------------+     
                                                             
```
- **Message Bus** (e.g., Kafka) provides decoupling.
- **Audit DB** can be any solution that scales writes/reads efficiently (e.g., Cassandra, PostgreSQL, etc., depending on compliance or data model).

### 4. **Live Feed Implementation**
- Each new action is published to the **audit service**.  
- The service can then **push** or broadcast it to **subscribed** user sessions (via WebSocket channels or SSE).
- For performance, consider a **Redis** pub/sub if you need an in-memory broadcast.

### 5. **Document Generation**
- On-demand or scheduled:
  - **On-demand**: The user triggers “Generate Audit Document,” the service queries the audit DB, then formats into PDF/CSV.
  - **Batch**: If many users request daily or monthly reports, a background service might pre-generate them.

### 6. **Performance and Scalability Considerations**
- **Write Path**:
  - The existing system must remain high-speed; ensure minimal synchronous overhead.  
  - Asynchronous event publication is common.
- **Read Path**:
  - Optimize frequent queries (e.g., user-based queries) with secondary indexes or time-based partitioning.
- **Data Retention**:
  - Determine how long logs are stored for compliance. Potentially move older logs to cheaper storage (tiered data approach).

### 7. **Edge Cases**
- **Network Failures**: If the audit service or message bus is down, ensure the trading system can buffer events or at least degrade gracefully.
- **Bulk Query**: A user requests the full transaction history from day one—need efficient pagination or chunked data retrieval.
- **Security & Permissions**: Only authorized personnel should see certain user actions. Possibly need access controls and encryption at rest.

---

## Conclusion
This stand-alone **audit service** needs:
1. **Event-driven ingestion** from the main trading system,
2. **Efficient data store** supporting high writes and quick queries,
3. **Real-time feed** mechanism for user action streaming,
4. **Document generation** for comprehensive history reports.

Maintaining **speed** and **reliability** is paramount. By decoupling the audit logic from the main system and using scalable data ingestion, you can ensure minimal impact on the core trading flow while still offering robust auditing features.
