flowchart TD
    A[Long Input Context<br/>(Prompt / Retrieved Docs / Article)]
        --> B[Tokenize Text]

    B --> B1[Map Tokens to Words]
    B1 --> C[Extract Embeddings]

    C --> D[Run First Attention Layer Only]
    D --> D1[Measure Relevance to Current Query]
    D --> D2[Measure Influence on Other Words]

    D1 --> E[Per-Word Importance Signals]
    D2 --> E

    E --> F[Aggregate Token Signals<br/>into Word Scores]

    F --> G[Smooth Keep / Drop Decisions<br/>(Sequential Model)]

    G --> H[Select Words to Keep]
    G --> I[Select Words to Drop]

    H --> J[Keep Relevant Context]
    I --> K[Remove Dropped Words<br/>from KV Cache]

    J --> L[Compact Context Memory]
    K --> L

    L --> M[Faster & Cheaper CPU Decoding]
