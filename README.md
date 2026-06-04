#Laboratorio1

##URL CODESPACE: https://symmetrical-fiesta-69rp9vvxpp5jfrqwp-8000.app.github.dev/

###Codigo Mermaid

´´´
graph TD
%% ========================================================
%% TITULO DEL DIAGRAMA: Arquitectura As-Is — FinTech Nova
%% ========================================================

%% ── ACTOR EXTERNO ─────────────────────────────────────
Cliente([👤 Cliente FinTech Nova<br/>App Movil / Web]):::actor

%% ── ZONA INTERNET ─────────────────────────────────────
subgraph Internet [🌐 INTERNET / Red Publica]
    Canal["HTTPS / TLS 1.3<br/>Puerto publico del Codespace"]
end

%% ── GITHUB CODESPACES ─────────────────────────────────
subgraph Codespaces [☁️ GitHub Codespaces | Microsoft Azure]
    subgraph Contenedor [📦 Contenedor Linux Efimero | VS Code Server]
        subgraph FastAPI [⚙️ FastAPI Application | uvicorn | Puerto 8000]
            EP1["POST /evaluar-riesgo<br/>Scoring Crediticio"]:::endpoint_safe
            EP2["GET /status<br/>Health Check"]:::endpoint_monitor
            EP3["GET /datos-financieros/{id}<br/>⚠️ VULNERABLE — Sin Autenticacion"]:::endpoint_vuln
        end
    end
end

%% ── CONEXIONES / FLUJOS ───────────────────────────────
Cliente -->|"HTTPS Request (JSON Payload)"| Canal
Canal -->|"HTTP interno (Puerto 8000)"| FastAPI
FastAPI -->|"Procesa request"| EP1
FastAPI -->|"Procesa request"| EP2
FastAPI -->|"Procesa request"| EP3

EP1 -.->|"JSON Response (Resultado)"| Cliente
EP2 -.->|"JSON Response (Healthy)"| Cliente
EP3 -.->|"JSON Response (⚠️ Historial expuesto)"| Cliente

%% ── ESTILOS ──────────────────────────────────────────
classDef actor fill:#EBF5FB,stroke:#1A5C9A,stroke-width:2px,color:#0D2B55
classDef endpoint_safe fill:#C8DDEF,stroke:#1A5C9A,stroke-width:2px,color:#0D2B55
classDef endpoint_monitor fill:#D5F5E3,stroke:#1E8449,stroke-width:2px,color:#1E8449
classDef endpoint_vuln fill:#FADBD8,stroke:#C0392B,stroke-width:3px,color:#C0392B

--------------------------------------------------------------------------------
´´´