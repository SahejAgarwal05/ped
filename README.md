flowchart TD
    %% =========================
    %% Input Stage
    %% =========================
    subgraph S1["Stage 1 · Input Context"]
        A["Long Input Context<br/>(Prompt · Retrieved Docs · Articles)"]
    end

    %% =========================
    %% Tokenization & Representation
    %% =========================
    subgraph S2["Stage 2 · Tokenization & Representation"]
        B["Tokenize Text"]
        B1["Map Tokens → Words"]
        C["Extract Token Embeddings"]
    end

    %% =========================
    %% Lightweight Importance Estimation
    %% =========================
    subgraph S3["Stage 3 · Lightweight Importance Estimation"]
        D["Run First Attention Layer Only"]
        D1["Relevance to Current Query"]
        D2["Influence on Neighboring Words"]
        E["Per-Word Importance Signals"]
        F["Aggregate Token Signals<br/>→ Word-Level Scores"]
    end

    %% =========================
    %% Decision Smoothing
    %% =========================
    subgraph S4["Stage 4 · Smooth Pruning Decision"]
        G["Sequential Keep / Drop Model<br/>(Smoothing & Consistency)"]
        H["Words to Keep"]
        I["Words to Drop"]
    end

    %% =========================
    %% Context Pruning
    %% =========================
    subgraph S5["Stage 5 · Context Pruning"]
        J["Retain Relevant Words"]
        K["Remove Dropped Words<br/>from KV Cache"]
        L["Compact Context Memory"]
    end

    %% =========================
    %% Output
    %% =========================
    subgraph S6["Stage 6 · Efficient Decoding"]
        M["Faster & Cheaper CPU Decoding"]
    end

    %% =========================
    %% Flow Connections
    %% =========================
    A --> B
    B --> B1 --> C
    C --> D
    D --> D1
    D --> D2
    D1 --> E
    D2 --> E
    E --> F
    F --> G
    G --> H
    G --> I
    H --> J
    I --> K
    J --> L
    K --> L
    L --> M

    %% =========================
    %% Styling
    %% =========================
    classDef input fill:#f9fafb,stroke:#111827,stroke-width:1.5px
    classDef process fill:#eef2ff,stroke:#1e40af,stroke-width:1.2px
    classDef decision fill:#ecfeff,stroke:#0f766e,stroke-width:1.2px
    classDef output fill:#f0fdf4,stroke:#166534,stroke-width:1.5px

    class A input
    class B,B1,C,D,D1,D2,E,F process
    class G,H,I decision
    class J,K,L,M output
