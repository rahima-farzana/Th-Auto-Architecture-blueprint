```mermaid
graph TD
    subgraph Users & Channels
        Agent[Agents / Brokers] -->|OneHub 3.0 / iPrompt| Gateway
        Cust[Customers] -->|MyChubb / LINE OA| Gateway
        Surv[External Surveyors] -->|Surveyor Mobile App| Gateway
    end

    subgraph Orchestration & API Management Layer [Azure APIM]
        Gateway[Chubb.io API Gateway]
    end

    subgraph Core Engines & Policy Lifecycle
        Gateway -->|OAuth 2.0| DC[DuckCreek Cloud]
        Gateway -->|Rating Enquiries| RL[RadarLive Engine]
        Gateway -->|OCR Scans| OCR[THOCR AppMan]
        Gateway -->|Vehicle Pricing| RB[Redbook API]
    end

    subgraph Claims Ecosystem
        Gateway -->|Claims Operations| CMX[CMX / NICE-AUTO]
        CMX -->|Procurement & STP| GP[GPOnline]
        GP -->|Clearance| EMCS[EMCS Platform]
        GP -->|Settlements| GPI[Global Payment Infra]
    end

    subgraph Data & Analytics
        DC & CMX & GP --> GDP[Global Data Platform]
        RefDB[(Azure SQL Reference Data)] --> Gateway
    end

    style Gateway fill:#1168bd,stroke:#0b4884,color:#fff
    style DC fill:#438dd5,stroke:#3069a1,color:#fff
    style CMX fill:#438dd5,stroke:#3069a1,color:#fff
    style GDP fill:#666,stroke:#333,color:#fff
