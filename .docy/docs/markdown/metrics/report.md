```mermaid
flowchart TD
    A[Start] --> B{Load Evaluation Logs}
    B --> C{Load Gold Results}
    C --> D{Calculate Metrics}
    D --> E{Generate Report}
    E --> F{Generate Summary}
    F --> G[End]

    subgraph get_eval_report
        D -->|Fail to Pass| F2P[Calculate F2P Metrics]
        D -->|Pass to Pass| P2P[Calculate P2P Metrics]
        D -->|Fail to Fail| F2F[Calculate F2F Metrics]
        D -->|Pass to Fail| P2F[Calculate P2F Metrics]
    end

    subgraph get_eval_reports_for_logs
        B -->|For Each Log| C
        C -->|Find Corresponding Gold Result| D
        D -->|For Each Test Case| E
    end

    subgraph get_eval_reports_for_dir
        A -->|Load Logs from Directory| B
    end

    subgraph get_model_eval_summary
        A -->|Load Predictions| preds[Load Predictions]
        preds -->|Filter by Repo| filter[Filter Predictions]
        filter -->|Get Reports| get_eval_reports_for_dir
        get_eval_reports_for_dir -->|Compile Summary| F
    end

    subgraph get_model_report
        A -->|Load Predictions| predictions[Load Predictions]
        predictions -->|For Each Prediction| check[Check Model Patch]
        check -->|Exists| exists[Model Patch Exists]
        exists -->|Log Exists| log_exists[Log File Exists]
        log_exists -->|Eval Log Found| found[Eval Log Found]
        found -->|Generate Report| get_eval_report
        get_eval_report -->|Resolution Status| resolution[Check Resolution Status]
        resolution -->|Compile Report| G
    end
```
This mermaid diagram illustrates the flow and functionalities of the provided code snippets, focusing on the evaluation report generation, model evaluation summary, and model report generation processes within the larger project context.