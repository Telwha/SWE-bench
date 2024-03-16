```mermaid
graph TD
    subgraph swe_bench_collect
        A[Start] --> B[get_top_pypi.py: Fetch PyPI Packages]
        B --> C[get_tasks_pipeline.py: Process Repositories]
        C --> D[print_pulls.py: Log Pull Requests]
        D --> E[utils.py: Utility Functions]
        E --> F[End]
    end

    subgraph cleanup
        G[cleanup: Start] --> H[delete_gh_workflows: Delete GitHub Workflows]
        H --> I[remove_envs: Remove Conda Environments]
        I --> J[cleanup: End]
    end

    subgraph make_repo
        K[make_repo: Start] --> L[call_make_repo.py: Initiate Repository Creation]
        L --> M[make_repo.sh: Create and Configure Repositories]
        M --> N[make_repo: End]
    end

    %% Connections between main tasks and cleanup/make_repo subgraphs
    F --> G : "Pre-cleanup"
    J --> K : "Post-cleanup, Pre-make_repo"
    N --> A : "Cycle back to start"

    style swe_bench_collect fill:#f9f,stroke:#333,stroke-width:4px
    style cleanup fill:#bbf,stroke:#f66,stroke-width:4px
    style make_repo fill:#bff,stroke:#333,stroke-width:4px
```