# Visual Guide to Load Balancing Algorithms

This guide provides visual representations of ten fundamental load balancing algorithms using Mermaid charts. Load balancing is essential for distributing incoming network traffic across multiple servers to ensure optimal resource utilization, minimize response time, and prevent overload. Each algorithm has a unique strategy for deciding which server should handle a given request.

## 1. Least Bandwidth

The least bandwidth algorithm forwards requests to the server currently handling the least amount of bandwidth.

```mermaid
graph TD
    subgraph Algorithm
        A[Start] --> B["Monitor bandwidth of all servers"]
        B --> C["Select server with<br/>least bandwidth usage"]
        C --> D["Forward request"]
        D --> E[End]
    end

    subgraph Servers
        F["Server 1: 10 Mbps"]
        G["Server 2: 5 Mbps"]
        H["Server 3: 8 Mbps"]
    end

    C -.-> G

    style F fill:#f9f,stroke:#333,stroke-width:2px
    style G fill:#bbf,stroke:#333,stroke-width:4px
    style H fill:#fbf,stroke:#333,stroke-width:2px
```

## 2. Agent-Based Adaptive Method

This algorithm dynamically adjusts load balancing decisions based on real-time feedback from agents monitoring server performance.

```mermaid
graph TD
    subgraph Algorithm
        A[Start] --> B["Gather performance metrics<br/>from agents"]
        B --> C["Analyze metrics (CPU, Memory, Load)"]
        C --> D["Select best server"]
        D --> E["Forward request"]
        E --> F[End]
    end

    subgraph Servers
        G["Server 1: CPU 30%, Load 2"]
        H["Server 2: CPU 80%, Load 6"]
        I["Server 3: CPU 50%, Load 4"]
    end

    D -.-> G

    style G fill:#bbf,stroke:#333,stroke-width:4px
    style H fill:#f9f,stroke:#333,stroke-width:2px
    style I fill:#fbf,stroke:#333,stroke-width:2px
```

## 3. Chained Failover

The chained failover algorithm sequentially forwards a request to the next available server until a successful response is received.

```mermaid
graph TD
    subgraph Algorithm
        A[Start] --> B["Forward request to primary server"]
        B --> C{"Request failed?"}
        C -->|Yes| D["Forward request to<br/>next server"]
        D --> C
        C -->|No| E[End]
    end

    subgraph Servers
        F["Server 1"]
        G["Server 2"]
        H["Server 3"]
    end

    B -.-> F
    D -.-> G
    D -.-> H

    style F fill:#f9f,stroke:#333,stroke-width:2px
    style G fill:#bbf,stroke:#333,stroke-width:4px
    style H fill:#fbf,stroke:#333,stroke-width:2px
```

## 4. Geographic Location-Based

This algorithm forwards a request to the server that is geographically closest to the client.

```mermaid
graph TD
    subgraph Algorithm
        A[Start] --> B["Identify client location"]
        B --> C["Select nearest server"]
        C --> D["Forward request"]
        D --> E[End]
    end

    subgraph Servers
        F["Server 1: North America"]
        G["Server 2: Europe"]
        H["Server 3: Asia"]
    end

    C -.->|Europe| G

    style F fill:#f9f,stroke:#333,stroke-width:2px
    style G fill:#bbf,stroke:#333,stroke-width:4px
    style H fill:#fbf,stroke:#333,stroke-width:2px
```

## 5. IP Hashing

IP hashing uses a hash function on the client's IP address to map each client to a specific server.

```mermaid
graph TD
    subgraph Algorithm
        A[Start] --> B["Compute hash(IP)"]
        B --> C["Determine server index:<br/>hash(IP) % total_servers"]
        C --> D["Forward request to server"]
        D --> E[End]
    end

    subgraph Servers
        F["Server 1"]
        G["Server 2"]
        H["Server 3"]
    end

    C -.->|Index 1| G

    style F fill:#f9f,stroke:#333,stroke-width:2px
    style G fill:#bbf,stroke:#333,stroke-width:4px
    style H fill:#fbf,stroke:#333,stroke-width:2px
```

## 6. Least Connections

The least connections algorithm forwards a request to the server with the fewest active connections.

```mermaid
graph TD
    subgraph Algorithm
        A[Start] --> B["Check active connections<br/>for each server"]
        B --> C["Select server with<br/>least connections"]
        C --> D["Forward request"]
        D --> E[End]
    end

    subgraph Servers
        F["Server 1: 15 Connections"]
        G["Server 2: 5 Connections"]
        H["Server 3: 10 Connections"]
    end

    C -.-> G

    style F fill:#f9f,stroke:#333,stroke-width:2px
    style G fill:#bbf,stroke:#333,stroke-width:4px
    style H fill:#fbf,stroke:#333,stroke-width:2px
```

## 7. Least Response Time

This algorithm selects the server with the shortest response time for the last few requests.

```mermaid
graph TD
    subgraph Algorithm
        A[Start] --> B["Measure response time<br/>for each server"]
        B --> C["Select server with<br/>least response time"]
        C --> D["Forward request"]
        D --> E[End]
    end

    subgraph Servers
        F["Server 1: 100ms"]
        G["Server 2: 50ms"]
        H["Server 3: 75ms"]
    end

    C -.-> G

    style F fill:#f9f,stroke:#333,stroke-width:2px
    style G fill:#bbf,stroke:#333,stroke-width:4px
    style H fill:#fbf,stroke:#333,stroke-width:2px
```

## 8. Round Robin

Round-robin distributes requests sequentially across all servers in the pool.

```mermaid
graph TD
    subgraph Algorithm
        A[Start] --> B["Select next server in sequence"]
        B --> C["Forward request"]
        C --> D["Update sequence index"]
        D --> E[End]
    end

    subgraph Servers
        F["Server 1"]
        G["Server 2"]
        H["Server 3"]
    end

    B -.-> F
    D -.-> G
    D -.-> H

    style F fill:#bbf,stroke:#333,stroke-width:4px
    style G fill:#fbf,stroke:#333,stroke-width:2px
    style H fill:#f9f,stroke:#333,stroke-width:2px
```

## 9. Weighted Least Connections

Weighted least connections takes into account server capacities by using weights when selecting the server with the fewest connections.

```mermaid
graph TD
    subgraph Algorithm
        A[Start] --> B["Check active connections<br/>for each server"]
        B --> C["Calculate weighted connections:<br/>connections / weight"]
        C --> D["Select server with<br/>least weighted connections"]
        D --> E["Forward request"]
        E --> F[End]
    end

    subgraph Servers
        G["Server 1: 10 / 2"]
        H["Server 2: 5 / 1"]
        I["Server 3: 15 / 3"]
    end

    D -.-> H

    style G fill:#f9f,stroke:#333,stroke-width:2px
    style H fill:#bbf,stroke:#333,stroke-width:4px
    style I fill:#fbf,stroke:#333,stroke-width:2px
```

## 10. Weighted Round Robin

Weighted round-robin forwards requests based on a predefined weight assigned to each server.

```mermaid
graph TD
    subgraph Algorithm
        A[Start] --> B["Assign weight to each server"]
        B --> C["Select server based on weight"]
        C --> D["Forward request"]
        D --> E[End]
    end

    subgraph Servers
        F["Server 1: Weight 2"]
        G["Server 2: Weight 1"]
        H["Server 3: Weight 3"]
    end

    C -.-> H

    style F fill:#f9f,stroke:#333,stroke-width:2px
    style G fill:#fbf,stroke:#333,stroke-width:2px
    style H fill:#bbf,stroke:#333,stroke-width:4px
```

This guide provides a comprehensive overview of the various load balancing strategies, offering a visual approach to understanding the strengths and differences of each method.
