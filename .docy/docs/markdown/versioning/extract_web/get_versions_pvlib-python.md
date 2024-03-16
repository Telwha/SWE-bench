```mermaid
graph TD
    A[Start] --> B(Get raw dataset)
    B --> C(Get version to date from webpage)
    C --> D{Iterate through matches}
    D --> E[Construct (version, date) pairs]
    E --> F[Group times by major/minor version]
    F --> G[Pick most recent time as version cut-off date]
    G --> H{Assign version to each task instance}
    H --> I[Construct map of versions to task instances]
    I --> J[Save versioned data to repository]
    J --> K[End]
```