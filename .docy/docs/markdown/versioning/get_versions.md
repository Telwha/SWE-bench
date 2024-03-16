```mermaid
graph TD
    A[Start] --> B{Parse Arguments}
    B --> C[Get Task Instances]
    C --> D{Split Instances for Threads}
    D --> E{Determine Retrieval Method}
    E -->|GitHub| F[Get Versions from Web]
    E -->|Build| G[Get Versions from Build]
    E -->|Mix| H[Get Versions from Web and Build]
    F --> I[Merge Results and Cleanup]
    G --> I
    H --> I
    I --> J[End]

    subgraph web "Web Version Retrieval"
        F --> F1[Search GitHub for Versions]
        F1 --> F2[Save Versions to File]
    end

    subgraph build "Build Version Retrieval"
        G --> G1[Setup Environment]
        G1 --> G2[Clone Repo and Conda Env per Thread]
        G2 --> G3[Build Repo and Retrieve Versions]
        G3 --> G4[Save Versions to File]
    end

    subgraph mix "Mixed Version Retrieval"
        H --> H1[Search GitHub for Versions]
        H1 --> H2[Filter Instances Not Found]
        H2 --> H3[Setup Environment]
        H3 --> H4[Clone Repo and Conda Env per Thread]
        H4 --> H5[Build Repo and Retrieve Versions]
        H5 --> H6[Save Versions to File]
    end
```