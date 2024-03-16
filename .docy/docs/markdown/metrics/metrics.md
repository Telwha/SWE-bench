```mermaid
graph TD
    A[Start] --> B[Compute Metrics]
    B --> C{Is it a single report?}
    C -->|Yes| D[Compute Single Report Metrics]
    C -->|No| E[Compute Multiple Reports Metrics]
    D --> D1[Compute Fail-to-Pass for Single Report]
    D --> D2[Compute Pass-to-Pass for Single Report]
    E --> E1{Is it weighted?}
    E1 -->|Yes| E2[Compute Weighted Metrics]
    E1 -->|No| E3[Compute Unweighted Metrics]
    E2 --> E2A[Compute Weighted Fail-to-Pass]
    E2 --> E2B[Compute Weighted Pass-to-Pass]
    E3 --> E3A[Compute Unweighted Fail-to-Pass]
    E3 --> E3B[Compute Unweighted Pass-to-Pass]
    D1 & D2 & E2A & E2B & E3A & E3B --> F[Get Resolution Status]
    F --> G{Determine Status}
    G -->|FULL| H[Resolved Full]
    G -->|PARTIAL| I[Resolved Partial]
    G -->|NO| J[Resolved No]
    H & I & J --> K[End]
```
This mermaid diagram illustrates the flow of operations within the provided code. It starts with the decision of whether the input is a single report or multiple reports, followed by further decisions based on the type of computation (weighted or unweighted for multiple reports) and concludes with determining the resolution status based on the computed metrics.