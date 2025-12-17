flowchart LR
    subgraph Source ["Landing (İniş)"]
        A[("Kirli CSV Dosyaları")] 
    end

    subgraph Colab ["Google Colab (İşlemci)"]
        P(Python & Pandas)
    end

    subgraph Storage ["Google Drive (Medallion Mimarisi)"]
        direction TB
        B[("🥉 Bronze Katman\n(Parquet - Ham Veri)")]
        C[("🥈 Silver Katman\n(Temiz Veri - Regex/Trim)")]
        D[("🥇 Gold Katman\n(Raporluk Veri - Star Schema)")]
    end

    subgraph Output ["Analiz & Raporlama"]
        E[("🦆 DuckDB\n(SQL Analizi)")]
        F[("📊 Dashboard\n(Tableau/DBeaver)")]
    end

    A -->|"Ingestion"| P
    P -->|"Raw Save"| B
    B -->|"Transformation"| P
    P -->|"Cleaning"| C
    C -->|"Aggregation"| P
    P -->|"Modelling"| D
    D -->|"Zero-Copy SQL"| E
    D -->|"Export CSV"| F

    style Source fill:#ffdddd,stroke:#333,stroke-width:2px
    style Storage fill:#e1f5fe,stroke:#0277bd,stroke-width:2px
    style Colab fill:#fff9c4,stroke:#fbc02d,stroke-width:2px,stroke-dasharray: 5 5
    style Output fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px
