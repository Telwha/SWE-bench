```mermaid
flowchart TD
    A[Start] --> B{Parse Issue URL}
    B -->|Valid| C[Get Problem Statement]
    B -->|Invalid| Z[Error: Invalid URL]
    C --> D[Clone Repository]
    D --> E[Build BM25 Retrieval Index]
    E --> F[Search in Index]
    F --> G{Include READMEs?}
    G -->|Yes| H[Get README Files]
    G -->|No| I[Skip READMEs]
    H --> J[Ingest Files]
    I --> J
    J --> K[Generate Prompt]
    K --> L[Call Model]
    L --> M[Extract Diff from Response]
    M --> N[Extract Minimal Patch]
    N --> O[Save Output]
    O --> P[End]
```
This flowchart represents the steps taken by the code to run a live inference session on a GitHub issue. It starts with parsing the issue URL, retrieving the problem statement, cloning the repository, and building a BM25 retrieval index. It then searches the index, decides whether to include README files, ingests files if necessary, and generates a prompt. The model is called with this prompt, and the response is processed to extract a diff and a minimal patch. Finally, the output is saved, and the process ends.