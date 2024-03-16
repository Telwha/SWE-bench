```mermaid
graph TD
    subgraph delete_gh_workflows
        A[Start] --> B{Parse Arguments}
        B --> C[Get List of Remote Branches]
        C --> D[Clone Repo to temp_repo]
        D --> E{For Each Branch}
        E -->|For Each| F[Switch to Branch]
        F --> G{Check .github/workflows Exists}
        G -->|Exists| H[Delete .github/workflows Folder]
        H --> I[Add Changes]
        I --> J[Commit Changes]
        J --> K[Push Changes]
        G -->|Does Not Exist| L[Print Folder Not Found]
        K --> M{More Branches?}
        L --> M
        M -->|Yes| F
        M -->|No| N[Cleanup: Delete temp_repo]
        N --> O[End]
    end

    subgraph remove_envs
        P[Start] --> Q{Parse Arguments}
        Q --> R[Get Conda Environments]
        R --> S{Check Each Environment}
        S -->|For Each| T[Remove Environment]
        T --> U[Delete Folders with Prefix]
        U --> V[End]
    end

    style delete_gh_workflows fill:#f9f,stroke:#333,stroke-width:2px
    style remove_envs fill:#bbf,stroke:#f66,stroke-width:2px

    %% Connections between subgraphs to illustrate potential workflow or dependencies
    %% Assuming these scripts might be part of a larger cleanup or setup process
    V --> A : "Subsequent Cleanup"
    O --> P : "Preceding Task"
```