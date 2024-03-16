```mermaid
graph TD
    A[Start] --> B[Import Dependencies]

    B --> C[Get Raw Astropy Dataset]
    C --> D[Get Version to Date from Astropy Homepage]

    D --> E[Extract (Date, Version) Pairs]
    E --> F[Construct (Version, Date) Pairs]
    F --> G[Group Times by Major/Minor Version]
    G --> H[Pick Most Recent Time as Version Cut Off Date]

    H --> I[Assign Version to Each Task Instance]
    I --> J[Construct Map of Versions to Task Instances]

    J --> K[Save Matplotlib Versioned Data to Repository]
    K --> L[End]
```