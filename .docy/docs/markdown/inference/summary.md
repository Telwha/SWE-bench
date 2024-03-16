```mermaid
flowchart TB
    subgraph inference_process ["Inference Process"]
        start((Start)) --> init_env[Initialize swe-bench Environment]
        init_env --> data_check{Check if Data Exists}
        data_check -->|Yes| load_data[Load Existing Data]
        data_check -->|No| create_data[Create New Data]
        load_data --> process_data[Process Data]
        create_data --> process_data
        process_data --> processing_complete{Is Processing Complete?}
        processing_complete -->|Yes| save_data[Save Processed Data]
        processing_complete -->|No| process_data
        save_data --> generate_reports[Generate Reports]
        generate_reports --> end((End))
    end

    subgraph model_processing ["Model Processing"]
        model_start((Start)) --> init_model[Initialize Model Components]
        init_model --> component_type{Component Type}
        component_type -->|Embed Tokens| embedding_layer[Embedding Layer]
        component_type -->|Model Layers| processing_layers[Processing Layers]
        component_type -->|Norm| normalization_layer[Normalization Layer]
        component_type -->|LM Head| language_model_head[Language Model Head]
        embedding_layer --> token_embedding_proc[Token Embedding Processing]
        processing_layers --> layer_wise_proc[Layer-wise Processing]
        normalization_layer --> normalization_proc[Normalization Processing]
        language_model_head --> language_model_output[Language Model Output]
        layer_wise_proc --> layer_activation{Layer Activation}
        layer_activation -->|0| no_activation[No Activation]
        layer_activation -->|1| activation_lvl1[Activation Level 1]
        layer_activation -->|2| activation_lvl2[Activation Level 2]
        layer_activation -->|3| activation_lvl3[Activation Level 3]
        no_activation --> output_next_layer[Output to Next Layer/Process]
        activation_lvl1 --> output_next_layer
        activation_lvl2 --> output_next_layer
        activation_lvl3 --> output_next_layer
        output_next_layer --> next_component{Next Component}
        next_component -->|Model Layers| processing_layers
        next_component -->|Norm| normalization_layer
        next_component -->|LM Head| language_model_head
        next_component -->|End| model_end((End of Model Processing))
    end

    subgraph environment_setup ["Environment Setup"]
        env_start((Start)) --> define_channels[Define Channels]
        define_channels --> define_dependencies[Define Dependencies]
        define_dependencies --> base_env_deps[Base Environment Dependencies]
        base_env_deps --> python_core_libs[Python and Core Libraries]
        python_core_libs --> dev_tools[Development Tools]
        dev_tools --> define_pip_deps[Define pip Dependencies]
        define_pip_deps --> core_python_libs[Core Python Libraries]
        core_python_libs --> data_ai_libs[Data Processing and AI Libraries]
        data_ai_libs --> web_net_libs[Web and Networking Libraries]
        web_net_libs --> dev_debug_tools[Development and Debugging Tools]
        dev_debug_tools --> env_end((End))
    end

    subgraph api_inference ["API Inference"]
        api_start((Start)) --> check_model_prefix{Check Model Prefix}
        check_model_prefix -->|claude| anthropic_inference[Anthropic Inference]
        check_model_prefix -->|gpt| openai_inference[OpenAI Inference]
        anthropic_inference --> load_dataset[Load Dataset]
        openai_inference --> load_dataset
        load_dataset --> filter_dataset{Filter Dataset}
        filter_dataset -->|Existing IDs| filter_existing_ids[Filter out existing IDs]
        filter_dataset -->|Shard Info| select_shard[Select Shard]
        filter_existing_ids --> select_shard
        select_shard --> inference_loop[Inference Loop]
        inference_loop --> check_max_cost{Check Max Cost}
        check_max_cost -->|Reached| exit[Exit]
        check_max_cost -->|Not Reached| inference_loop
        exit --> api_end((End))
    end

    subgraph live_inference ["Live Inference"]
        live_start((Start)) --> parse_issue_url{Parse Issue URL}
        parse_issue_url -->|Valid| get_problem_statement[Get Problem Statement]
        parse_issue_url -->|Invalid| error_invalid_url[Error: Invalid URL]
        get_problem_statement --> clone_repo[Clone Repository]
        clone_repo --> build_bm25_index[Build BM25 Retrieval Index]
        build_bm25_index --> search_index[Search in Index]
        search_index --> include_readmes{Include READMEs?}
        include_readmes -->|Yes| get_readme_files[Get README Files]
        include_readmes -->|No| skip_readmes[Skip READMEs]
        get_readme_files --> ingest_files[Ingest Files]
        skip_readmes --> ingest_files
        ingest_files --> generate_prompt[Generate Prompt]
        generate_prompt --> call_model[Call Model]
        call_model --> extract_diff[Extract Diff from Response]
        extract_diff --> extract_minimal_patch[Extract Minimal Patch]
        extract_minimal_patch --> save_output[Save Output]
        save_output --> live_end((End))
    end

    subgraph dataset_preparation ["Dataset Preparation"]
        ds_start((Start)) --> init_bench_env[Initialize Benchmark Environment]
        init_bench_env --> bm25_retrieval[BM25 Dataset Retrieval]
        init_bench_env --> create_instance[Create Instance]
        init_bench_env --> create_text_dataset[Create Text Dataset]
        init_bench_env --> tokenize_dataset[Tokenize Dataset]
        init_bench_env --> util_funcs[Utility Functions]
        bm25_retrieval --> create_text_dataset
        create_instance --> create_text_dataset
        tokenize_dataset --> create_text_dataset
        util_funcs --> create_instance
        util_funcs --> bm25_retrieval
        create_text_dataset --> ds_end((End))
    end

    inference_process --> model_processing --> environment_setup --> api_inference --> live_inference --> dataset_preparation
```