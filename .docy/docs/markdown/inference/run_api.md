```mermaid
flowchart TD
    A[Start] --> B{Check Model Prefix}
    B -->|claude| C[Anthropic Inference]
    B -->|gpt| D[OpenAI Inference]
    C --> E[Load Dataset]
    D --> E
    E --> F{Filter Dataset}
    F -->|Existing IDs| G[Filter out existing IDs]
    F -->|Shard Info| H[Select Shard]
    G --> H
    H --> I[Inference Loop]
    I --> J{Check Max Cost}
    J -->|Reached| K[Exit]
    J -->|Not Reached| I
    K --> L[End]
```

This flowchart represents the high-level logic of the provided code. The process starts with determining the model prefix to decide whether to use the Anthropic or OpenAI inference path. After loading and optionally filtering the dataset based on existing IDs and shard information, it enters an inference loop. Within this loop, it checks if the maximum cost has been reached after each inference call. If the max cost is reached, the process exits; otherwise, it continues with the next inference call until completion.