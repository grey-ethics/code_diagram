# Code Diagram

Lightweight repo to keep architecture and flow diagrams next to code.

## Live diagrams (rendered by GitHub)

### Architecture (Mermaid – C4-style)
```mermaid
flowchart LR
  subgraph Browser
    FE[React SPA]
  end
  subgraph VPC
    BE[(FastAPI Backend)]
    DB[(PostgreSQL)]
    MCP[(MCP Server)]
    LLM[(LLM Service)]
  end
  FE <--> BE
  BE <--> DB
  BE <--> MCP
  BE <--> LLM

flowchart TD
  A[Load App] --> B[GET /catalog]
  B --> C{User picks tool card?}
  C -- Formula 1 --> D[Render form (a,b)]
  D --> E[Submit] --> F[POST /tools/invoke]
  F --> G[Validate/Auth] --> H{Adapter}
  H -- Local --> I[services.formula_1]
  H -- MCP --> J[MCP call formula_1]
  I --> K[Result]
  J --> K
  K --> L[Return to FE]