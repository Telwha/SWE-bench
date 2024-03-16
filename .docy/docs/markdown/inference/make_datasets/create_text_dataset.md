```mermaid
graph TD
    A[Start] --> B[Parse Arguments]
    B --> C{Check push_to_hub_user}
    C -->|None| D[Create output directory if not exists]
    C -->|Not None| E[Check HUGGING_FACE_HUB_TOKEN and output_dir]
    B --> F{Check max_context_len}
    F -->|Not None| G[Assert tokenizer_name is not None]
    B --> H[Generate output file name based on arguments]
    H --> I{Check if dataset exists on disk}
    I -->|Yes| J[Load dataset from disk]
    I -->|No| K[Load dataset from HuggingFace Datasets]
    K --> L[Process each split in dataset]
    L --> M[Add text inputs to instances]
    M --> N[Extract fields from instances]
    N --> O[Create Dataset from processed data]
    O --> P{Check validation_ratio}
    P -->|>0| Q[Split train dataset into train and validation]
    P -->|<=0| R[Proceed without splitting]
    Q --> S[Log number of instances per split]
    R --> S
    S --> T{Check push_to_hub_user}
    T -->|Not None| U[Push dataset to HuggingFace Hub]
    T -->|None| V[Save dataset to disk]
    U --> W[End]
    V --> W
```
This mermaid diagram illustrates the flow of operations in the provided code snippet. It starts with parsing command-line arguments, checks conditions related to `push_to_hub_user` and `max_context_len`, and decides on the dataset loading strategy. It then processes each dataset split by adding text inputs, extracting necessary fields, and creating a `Dataset` object. Depending on the `validation_ratio`, it may split the training dataset. Finally, it either pushes the dataset to the HuggingFace Hub or saves it to disk, based on the `push_to_hub_user` argument.