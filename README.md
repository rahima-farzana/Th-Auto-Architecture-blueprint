# APAC Auto Architecture Modernization Blueprint

## Executive Overview
Strategic blueprint to transform and scale the localized APAC Auto portfolio into a cloud-native, multi-market template. Designed to support expansion from Thailand to Malaysia, targeting a combined operating ratio (COR) of **96.1%** and a scale of **$70M → $360M** by 2028.

## System Topology & Micro-Frontend Architecture
graph TD
    User([Agent / Broker / Customer]) -->|HTTPS / OAuth 2.0| OneHub[OneHub 3.0: Angular Micro-Frontends]
    OneHub -->|BFF Pattern| ChubbIO[Chubb.io API Gateway / APIM Layer]
    
    subgraph Core Platforms
        ChubbIO -->|Orchestrated APIs| DC[DuckCreek Policy Cloud]
        ChubbIO -->|The Zero-Snowflake Rule| Radar[RadarLive Rating Engine]
    end
    
    subgraph Claims Ecosystem
        ChubbIO -->|REST / Push| NICE[NICE-Auto Core Claims]
        NICE --> GP[GPOnline / Garage Procurement]
        EMCS[(Third-Party EMCS File Dump)] -->|Tactical SFTP Bridge| GP
    end
    
    subgraph Security Perimeter
        Vault[(Azure Key Vault)] -.->|90-Day Rotation| ChubbIO
        CyberArk[CyberArk PAM] -.->|Service Accounts| DC
    end
    ## Key Architecture Decisions (ADRs)
* **ADR-001: The Zero-Snowflake Rule:** Centralized all calculation logic (Net/Gross Premium, Commission, VAT, Stamp Duty) inside RadarLive. Localized front-ends are strictly processing-prohibited.
* **ADR-002: Tactical Batch Ingestion:** Implemented a secure SFTP file bridge for EMCS data due to Day 1 API unavailability, abstracting the service layer for future REST conversion.
