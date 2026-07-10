# Mermaid Diagram Templates for Vault Notes

Reusable Mermaid diagram templates. Match the type to the content and adapt node labels.

## State Machine (stateDiagram-v2)

**Use for**: Protocol state machines, lifecycle flows, process states.

```mermaid
stateDiagram-v2
    [*] --> Idle
    Idle --> Active: 事件触发
    Active --> Processing: 条件满足
    Processing --> Done: 完成
    Processing --> Error: 失败
    Error --> Idle: 重试/恢复
    Done --> [*]
    note right of Active
        在此阶段可选说明
    end note
```

**OCF 模式模板**:
```text
[*] --> Initial
Initial --> Ready: condition1
Ready --> Running: condition2
Running --> Completed: success
Running --> Failed: error
Failed --> Ready: retry
Completed --> [*]
```

## Network Topology (graph TD)

**Use for**: Network diagrams, component architecture, node relationships.

```mermaid
graph TD
    Router1(["Router1<br/>RID 1.1.1.1"])
    Router2(["Router2<br/>RID 2.2.2.2"])
    Router3(["Router3<br/>RID 3.3.3.3"])

    Router1 ---|"Link Type"| Router2
    Router2 ---|"Link Type"| Router3

    class R1,R2,R3 nodeClass
    classDef nodeClass fill:#cce5ff,stroke:#007bff,stroke-width:2px,color:#000
```

## Data Flow (graph LR)

**Use for**: Packet flow, forwarding process, data pipeline.

```mermaid
graph LR
    Source["Source Label"] -->|"① Action"| Hop1["Hop 1 Label"]
    Hop1 -->|"② Action"| Hop2["Hop 2 Label"]
    Hop2 -->|"③ Action"| Dest["Dest Label"]

    class Source,Dest edgeNode
    class Hop1,Hop2 middleNode
    classDef edgeNode fill:#cce5ff,stroke:#007bff,stroke-width:2px,color:#000
    classDef middleNode fill:#e2e3e5,stroke:#6c757d,color:#000
```

## Dependency Graph (graph TD with title)

**Use for**: Course chapter dependencies, concept prerequisites.

```mermaid
---
title: Title Here
---
graph TD
    A[Chapter A] --> B[Chapter B]
    A --> C[Chapter C]
    B --> D[Chapter D]
    C --> D

    classDef chapter fill:#1a1a2e,stroke:#e94560,color:#eee
    class A,B,C,D chapter
```

## Styling Quick Reference

| Style | Fill | Stroke | Use for |
|-------|------|--------|---------|
| `fill:#cce5ff,stroke:#007bff` | Light blue | Blue | Primary nodes, routers, LER |
| `fill:#d4edda,stroke:#28a745` | Light green | Green | Client nodes, secondary |
| `fill:#fff3cd,stroke:#ffc107` | Light yellow | Yellow | Non-client, DR/BDR |
| `fill:#e2e3e5,stroke:#6c757d` | Light gray | Gray | Intermediate, LSR |
| `fill:#1a1a2e,stroke:#e94560,color:#eee` | Dark navy | Red | Chapter nodes (dark bg) |

## Shape Quick Reference

| Syntax | Shape | Example |
|--------|-------|---------|
| `A["text"]` | Rectangle | `NC["非 Client"]` |
| `A(["text"])` | Rounded rectangle | `RR(["路由反射器"])` |
| `A{"text"}` | Diamond (decision) | `Cond{"条件判断"}` |
| `A[["text"]]` | Stadium (pill) | `Db[["Database"]]` |

## References

- [Mermaid Official Docs](https://mermaid.js.org/syntax/)
- [Mermaid Live Editor](https://mermaid.live/)