# E-Munshi — Product Requirements Document (PRD)
### Version 1.0 · October 2026 · Confidential

---

<table>
<tr><td><strong>Product Name</strong></td><td>E-Munshi — AI-Powered Financial Intelligence for Tally</td></tr>
<tr><td><strong>Engineering Lead</strong></td><td>Mr.Aaquib Nawab</td></tr>
<tr><td><strong>Target Pilot Launch</strong></td><td>30 calendar days from project kickoff</td></tr>
<tr><td><strong>Last Updated</strong></td><td>October 26, 2026</td></tr>
</table>

---


## 1. Executive Summary

**E-Munshi** ("Munshi" — the trusted business bookkeeper in Hindi) is an AI-powered financial intelligence SaaS platform designed to bridge the **information access gap** between India's 7+ million Tally ERP users and their own accounting data.

### The Core Problem

Today, a business owner who wants to know "How much cash can I safely spend this month?" must open Tally, navigate complex menus, export data to Excel, WhatsApp it to their accountant, wait 2–3 days, and still receive an incomplete answer. **E-Munshi reduces this to a single natural-language question answered in under 5 seconds**, backed by deterministic computations on verified Tally data — not AI guesses.

### What We're Building (Pilot Scope)

A production-grade platform consisting of:

| Component | Description |
| :--- | :--- |
| **Local Tally Connector** | A lightweight, read-only Windows desktop agent that securely syncs data from TallyPrime/ERP 9 to the E-Munshi cloud |
| **Cloud Backend** | A multi-tenant API service with deterministic financial engines that guarantee computational accuracy |
| **AI Chat Interface** | A natural-language conversational assistant where users ask questions about their Tally data and receive source-cited, accurate answers |
| **Web Dashboard** | A modern financial dashboard with real-time KPIs, receivables aging, P&L summaries, and interactive reports |

### Why This Project Should Move Forward

| Dimension | Value Proposition |
| :--- | :--- |
| **Market Size** | 7M+ Tally installations in India; ~₹3,500 crore addressable accounting tech market |
| **Validated Demand** | Competitor Riko AI already serving paying customers, proving product-market fit |
| **Cost Efficiency** | Total pilot infrastructure: under ₹6,000/month; total 3-month cost under ₹30,000 |
| **Time to Market** | 30-day delivery to pilot-ready state with 3+ real users |
| **Revenue Model** | SaaS subscriptions starting at ₹399/month per company (entry), scaling to ₹18,000/year for CA firms |

---

## 2. Product Vision & Problem Statement

### Vision Statement

> *"Every Indian business owner should be able to understand their financial position in plain language — without depending on an accountant's availability, without learning complex software, and without compromising the accuracy of their books."*

### Problem Statement

Indian MSMEs face a fundamental **information asymmetry**: their financial data lives inside Tally, but extracting actionable insights requires:
- Technical proficiency in navigating Tally's report menus
- Availability of a qualified accountant or CA to interpret the data
- Manual export-to-Excel workflows prone to errors and delays
- 2–5 day turnaround times for even simple questions

This delay leads to:
- **Poor cash management** — owners don't know real-time cash positions
- **Lost revenue** — overdue receivables not followed up promptly
- **Missed compliance** — GST filing deadlines approached with incomplete data
- **Decision paralysis** — strategic decisions made on gut feeling, not data

### How E-Munshi Solves This

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                         THE INFORMATION ACCESS GAP                              │
│                                                                                 │
│  Business Owner wants: "How much cash can I safely spend this month?"           │
│                                                                                 │
│  TODAY (without E-Munshi)                    WITH E-Munshi                      │
│  ─────────────────────────────────────       ─────────────────────────         │
│  1. Open Tally Prime                         1. Open E-Munshi web app           │
│  2. Navigate to correct report               2. Type the question in chat       │
│  3. Set date range manually                  3. Receive answer with sources     │
│  4. Export to Excel                          ── 3 steps · under 5 seconds ──   │
│  5. Send to accountant on WhatsApp                                              │
│  6. Wait 2-3 days for reply                                                     │
│  7. Get partial answer                                                          │
│  8. Make decision with uncertainty                                              │
│  ── 8 steps · 2-3 days · information loss ──                                   │
└─────────────────────────────────────────────────────────────────────────────────┘
```


## 4. Scope & Boundaries

### In Scope — Pilot v1 (30 Days)

| # | Feature Area | Specific Deliverables |
| :--- | :--- | :--- |
| **F1** | Tally Data Sync | Local Windows connector; read-only; delta sync every 15 min; supports TallyPrime + ERP 9 |
| **F2** | User Authentication | Email/password + Google OAuth; JWT sessions; multi-tenant organization model |
| **F3** | Multi-Company Support | Company selector dropdown; per-company data isolation; sync status per company |
| **F4** | Financial Dashboard | Cash & bank balance card, Sales vs. Last Month, Top Debtors chart, Overdue Bills summary |
| **F5** | AI Chat Interface | Natural-language queries; 10 supported query types; SSE streaming; source-cited answers |
| **F6** | Deterministic Financial Engine | Receivables aging (0-30/31-60/61-90/90+), P&L, Trial Balance, Cash Flow, Period Comparison |
| **F7** | Report Viewing | Trial Balance, Profit & Loss, Outstanding Bills, Ledger Statement — all with data freshness labels |
| **F8** | Basic Exports | XLSX and PDF export for standard reports; S3 pre-signed download links |
| **F9** | Role-Based Access | Owner, Accountant, Viewer roles per organization |
| **F10** | Data Freshness Indicators | Every data point shows "as of HH:MM" timestamp; stale data warning when connector is offline |
| **F11** | Audit Logging | Every query, report fetch, and sync event logged with user, timestamp, company context |
| **F12** | Security Hardening | PostgreSQL RLS, JWT rotation, rate limiting, prompt injection defense, cross-tenant testing |

### Out of Scope — Deferred to v2

| # | Feature | Reason for Deferral |
| :--- | :--- | :--- |
| **D1** | Write to Tally (create vouchers/ledgers) | Catastrophic risk if buggy; requires full approval workflow, rollback, and audit. Deferred for safety. |
| **D2** | WhatsApp Business Bot | Requires WhatsApp Business API approval (2–4 week process); not blocking pilot value |
| **D3** | GST Reconciliation (GSTR-2A/2B matching) | Requires GSTN API integration + portal scraping; complex; separate sub-project |
| **D4** | Bank Reconciliation | Requires bank statement import/parsing; multiple formats; deferred |
| **D5** | Monthly MIS Auto-Generation | Requires template engine + scheduled jobs; v2 feature |
| **D6** | Mobile Native App (Android/iOS) | PWA covers mobile access in v1; native app if user demand warrants |
| **D7** | Payment Reminder Automation | Requires WhatsApp integration (D2) + template approval |
| **D8** | Inventory / Stock Analysis (Advanced) | Basic stock summary in v1; advanced BOM/costing deferred |
| **D9** | Multi-language UI (Hindi, Gujarati) | English-only UI for pilot; AI chat supports Hinglish queries |
| **D10** | White-Label / Custom Branding for CA Firms | Architecture supports it; UI implementation deferred |

### Explicit Non-Goals

- E-Munshi **does not replace Tally**. It is a companion intelligence layer.
- E-Munshi **does not perform bookkeeping**. It does not create or modify accounting entries in v1.
- E-Munshi **does not provide tax advice**. Financial data is presented for informational purposes; tax decisions remain with the CA.
- E-Munshi **does not store original Tally data files**. It stores structured, indexed copies of transactional data.

---

## 5. Functional Requirements

### FR-1: Tally Local Connector

| ID | Requirement | Priority | Acceptance Criteria |
| :--- | :--- | :--- | :--- |
| FR-1.1 | Connector installs as a single Windows `.exe` without requiring Node.js, Python, or other runtimes | P0 | Clean Windows 10/11 install succeeds without pre-requisites |
| FR-1.2 | Connector runs as a Windows system tray application with status indicator | P0 | Tray icon shows: 🟢 Connected, 🟡 Syncing, 🔴 Offline |
| FR-1.3 | Connector communicates with Tally via HTTP XML on localhost:9000 | P0 | Successfully queries TallyPrime and Tally.ERP 9 (Release 6+) |
| FR-1.4 | Connector uses outbound-only WebSocket (WSS) — no inbound ports opened | P0 | Network scan confirms zero listening ports created by connector |
| FR-1.5 | Initial full sync extracts: company list, chart of accounts, current year vouchers, bill-wise outstanding | P0 | Extracted data matches Tally's own reports for test dataset |
| FR-1.6 | Delta sync runs every 15 minutes, using `ALTEREDID` watermark for incremental extraction | P0 | Only changed records transferred after initial sync |
| FR-1.7 | Connector handles Tally offline gracefully (retry with exponential backoff) | P0 | No crash; connector retries and resumes when Tally restarts |
| FR-1.8 | All write operations are hard-blocked (`BLOCK_WRITE=1`) | P0 | Attempting any write operation returns error and is logged |
| FR-1.9 | Connector pairing uses a one-time token with 10-minute expiry | P0 | Expired token rejected; used token rejected on reuse |
| FR-1.10 | Sync progress shown in system tray tooltip during initial sync | P1 | User can see "Syncing ledgers... 2,341 of 5,120" |
| FR-1.11 | Connector logs stored locally with 30-day rotation | P1 | Diagnostic logs accessible for troubleshooting |

### FR-2: Authentication & User Management

| ID | Requirement | Priority | Acceptance Criteria |
| :--- | :--- | :--- | :--- |
| FR-2.1 | User can register with email + password | P0 | Account created; email verification sent |
| FR-2.2 | User can sign in with Google OAuth 2.0 (PKCE flow) | P0 | Google login redirects back with valid session |
| FR-2.3 | JWT access tokens expire in 15 minutes; refresh tokens in 7 days | P0 | Expired access token returns 401; refresh token issues new pair |
| FR-2.4 | User can create an organization and invite team members | P0 | Org created; invite link generated with role assignment |
| FR-2.5 | Three roles supported: OWNER (full access), ACCOUNTANT (data + reports), VIEWER (read-only dashboards) | P0 | Each role sees appropriate UI; unauthorized actions return 403 |
| FR-2.6 | User can be a member of multiple organizations | P1 | Org switcher in navigation; data isolation between orgs |

### FR-3: Financial Dashboard

| ID | Requirement | Priority | Acceptance Criteria |
| :--- | :--- | :--- | :--- |
| FR-3.1 | Dashboard shows Cash & Bank Balance for selected company | P0 | Amount matches Tally's Balance Sheet → Cash + Bank group |
| FR-3.2 | Dashboard shows Sales This Month vs. Last Month with % change | P0 | Sales figures match Tally's P&L → Sales Accounts total |
| FR-3.3 | Dashboard shows Top 5 Debtors by outstanding amount | P0 | Names and amounts match Tally's Bills Outstanding report |
| FR-3.4 | Dashboard shows Overdue Bills summary (count + total amount by aging bucket) | P0 | Aging buckets: 0–30, 31–60, 61–90, 90+ days; totals match manual verification |
| FR-3.5 | Company selector dropdown with sync status badge per company | P0 | Switching company refreshes all dashboard data |
| FR-3.6 | Data freshness badge on every metric ("As of 14:23 today") | P0 | Timestamp reflects actual sync time, not query time |
| FR-3.7 | Stale data warning when connector is offline for >30 minutes | P0 | Visible ⚠ badge with message: "Tally connector offline since HH:MM" |
| FR-3.8 | Quick action chips: "Show P&L", "Who owes me?", "Cash position" | P1 | Clicking chip navigates to chat with pre-filled question |

### FR-4: AI Chat Interface

| ID | Requirement | Priority | Acceptance Criteria |
| :--- | :--- | :--- | :--- |
| FR-4.1 | User types a natural-language question and receives a financial answer | P0 | "What is my cash balance?" returns correct ₹ amount with source |
| FR-4.2 | Response includes source citation: report type, data timestamp, company name | P0 | Every answer has "Source: [Report], as of [DateTime]" footer |
| FR-4.3 | Response streams progressively via Server-Sent Events (SSE) | P0 | User sees "Fetching data..." → "Computing..." → streamed answer |
| FR-4.4 | 10 supported query types in pilot (see tool allowlist in §10) | P0 | Each of the 10 tools returns verified results for test queries |
| FR-4.5 | Unsupported queries receive a polite, structured refusal with suggestion | P0 | "I can't help with GST filing yet. Try: 'Show my P&L for this month'" |
| FR-4.6 | Suggested follow-up questions appear after each answer | P1 | 2–3 contextual follow-ups shown as clickable chips |
| FR-4.7 | Chat history persists within a session; sessions list visible in sidebar | P1 | User can revisit past conversations |
| FR-4.8 | Chat supports Hinglish queries | P1 | "Mera cash balance kya hai?" returns same result as English equivalent |

### FR-5: Reports

| ID | Requirement | Priority | Acceptance Criteria |
| :--- | :--- | :--- | :--- |
| FR-5.1 | Trial Balance report with date range selection | P0 | Debit and Credit totals match Tally exactly |
| FR-5.2 | Profit & Loss report with period selection | P0 | Net Profit matches Tally's P&L |
| FR-5.3 | Outstanding Bills (Receivable + Payable) with aging bands | P0 | Party-wise outstanding with color-coded aging |
| FR-5.4 | Ledger Statement for any ledger with date range | P0 | Opening balance, each transaction, running balance, closing balance |
| FR-5.5 | Stock Summary (basic) | P1 | Item-wise stock quantities and values |
| FR-5.6 | Export any report to XLSX | P0 | Downloaded Excel file contains same data as screen |
| FR-5.7 | Export any report to PDF | P1 | Clean, branded PDF suitable for sharing |

### FR-6: Connector Management

| ID | Requirement | Priority | Acceptance Criteria |
| :--- | :--- | :--- | :--- |
| FR-6.1 | Settings page shows connector status: Online/Offline with last heartbeat time | P0 | Status updates within 60 seconds of connector state change |
| FR-6.2 | Connector pairing flow: generate token → enter in connector → connection established | P0 | New user can pair connector within 3 minutes following on-screen steps |
| FR-6.3 | Sync history: list of sync runs with status, record count, duration | P1 | User can see when syncs succeeded/failed and how many records synced |
| FR-6.4 | Connector download button with OS-appropriate installer | P0 | Single-click download of Windows .exe |

---

## 6. Non-Functional Requirements

### NFR-1: Performance

| ID | Requirement | Target |
| :--- | :--- | :--- |
| NFR-1.1 | Dashboard page load (after authentication) | < 2 seconds |
| NFR-1.2 | AI chat response time (question to first streamed token) | < 3 seconds (P50), < 5 seconds (P95) |
| NFR-1.3 | Report rendering (Trial Balance, P&L) | < 2 seconds for companies with < 50,000 vouchers |
| NFR-1.4 | Initial Tally sync (5,000 vouchers) | < 5 minutes |
| NFR-1.5 | Initial Tally sync (50,000 vouchers) | < 30 minutes |
| NFR-1.6 | Delta sync (incremental update) | < 30 seconds for < 500 changed records |
| NFR-1.7 | API response time (non-chat endpoints) | < 500ms (P95) |

### NFR-2: Availability & Reliability

| ID | Requirement | Target |
| :--- | :--- | :--- |
| NFR-2.1 | Cloud service uptime (API + web) | 99.5% (monthly) |
| NFR-2.2 | Database backup frequency | Automated daily; 7-day retention |
| NFR-2.3 | Disaster recovery RTO | < 4 hours |
| NFR-2.4 | Connector auto-reconnect after network drop | Within 60 seconds |
| NFR-2.5 | Zero data loss during sync interruptions | Resume from last watermark; no duplicates |

### NFR-3: Scalability (Pilot Targets)

| ID | Requirement | Target |
| :--- | :--- | :--- |
| NFR-3.1 | Concurrent users (pilot) | 50 simultaneous users |
| NFR-3.2 | Tally companies per organization | Up to 20 |
| NFR-3.3 | Vouchers per company | Up to 500,000 |
| NFR-3.4 | Chat queries per day (pilot) | Up to 5,000 |

### NFR-4: Security (Detailed in §11)

| ID | Requirement | Target |
| :--- | :--- | :--- |
| NFR-4.1 | Data at rest encryption | AES-256 (AWS RDS default) |
| NFR-4.2 | Data in transit encryption | TLS 1.2+ on all connections |
| NFR-4.3 | Multi-tenant isolation | PostgreSQL Row-Level Security + application-layer enforcement |
| NFR-4.4 | PII handling | PAN, GST, bank account numbers masked in logs and never sent to LLM |
| NFR-4.5 | Cross-tenant data access | Zero tolerance — automated test must pass before each release |

### NFR-5: Compatibility

| ID | Requirement | Target |
| :--- | :--- | :--- |
| NFR-5.1 | Tally versions supported | TallyPrime 2.x–5.x, Tally.ERP 9 (Release 6+) |
| NFR-5.2 | Connector OS support | Windows 10, Windows 11 (64-bit) |
| NFR-5.3 | Web browser support | Chrome 90+, Edge 90+, Firefox 90+, Safari 15+ |
| NFR-5.4 | Mobile web support | Responsive PWA on Android Chrome, iOS Safari |

### NFR-6: Maintainability

| ID | Requirement | Target |
| :--- | :--- | :--- |
| NFR-6.1 | Code test coverage (backend financial engine) | > 80% line coverage |
| NFR-6.2 | API documentation | Auto-generated OpenAPI (Swagger) spec |
| NFR-6.3 | Deployment process | Automated CI/CD via GitHub Actions |
| NFR-6.4 | Rollback capability | One-command rollback to previous version |

---

## 7. User Stories & Acceptance Criteria

### Epic 1: Tally Data Connection

**US-1.1** — *As a business owner, I want to download and install the E-Munshi connector on my Windows PC so that my Tally data is available in E-Munshi.*

| Criteria | Condition |
| :--- | :--- |
| **Given** | I am logged into E-Munshi web app and Tally is running on my PC |
| **When** | I download the connector, run it, and enter the pairing code shown on screen |
| **Then** | The connector connects to Tally, syncs my data, and my dashboard shows financial metrics within 10 minutes |
| **And** | No inbound ports are opened on my PC; no network configuration required |

**US-1.2** — *As a business owner, I want to see when my Tally data was last synced so that I know if the numbers are current.*

| Criteria | Condition |
| :--- | :--- |
| **Given** | I am viewing the dashboard |
| **When** | I look at any financial metric |
| **Then** | I see a timestamp showing when the data was last synced (e.g., "As of 14:23 today") |
| **And** | If the connector is offline, I see a warning: "⚠ Tally connector offline since [time]" |

---

### Epic 2: Financial Intelligence Queries

**US-2.1** — *As a business owner, I want to ask "What is my cash balance?" in plain English and receive an accurate answer.*

| Criteria | Condition |
| :--- | :--- |
| **Given** | My Tally data has been synced |
| **When** | I type "What is my cash balance?" in the chat |
| **Then** | I receive the exact cash + bank balance matching Tally's Balance Sheet |
| **And** | The answer includes source citation (report type, date, company name) |
| **And** | If data is stale, the answer includes a freshness warning |

**US-2.2** — *As a business owner, I want to know which customers owe me money and for how long, so I can follow up on collections.*

| Criteria | Condition |
| :--- | :--- |
| **Given** | Outstanding bills data has been synced |
| **When** | I ask "Who owes me the most money?" |
| **Then** | I receive a ranked list of debtors with outstanding amounts and aging (days overdue) |
| **And** | Amounts are computed deterministically (not by AI) and match Tally's Bills Outstanding report |

**US-2.3** — *As a CA managing multiple clients, I want to switch between companies and ask the same question across different books.*

| Criteria | Condition |
| :--- | :--- |
| **Given** | I have multiple Tally companies connected |
| **When** | I select a different company from the dropdown |
| **Then** | All dashboard data and chat context switch to the selected company |
| **And** | I cannot accidentally view data from a company I'm not authorized to access |

---

### Epic 3: Financial Reports

**US-3.1** — *As a finance manager, I want to view a Profit & Loss statement for any date range and export it to Excel.*

| Criteria | Condition |
| :--- | :--- |
| **Given** | I am on the Reports page |
| **When** | I select "Profit & Loss" and set the date range |
| **Then** | The P&L displays with proper Revenue / Expense grouping and Net Profit total |
| **And** | Net Profit matches Tally's own P&L for the same period |
| **And** | I can click "Export to Excel" and download the report |

**US-3.2** — *As a business owner, I want to see a receivables aging report showing which bills are overdue and by how much time.*

| Criteria | Condition |
| :--- | :--- |
| **Given** | Bill-wise outstanding data has been synced |
| **When** | I view the Outstanding Bills report |
| **Then** | Bills are grouped by party with aging buckets: 0–30, 31–60, 61–90, 90+ days |
| **And** | Each bucket shows count and total amount, color-coded by severity |

---

### Epic 4: Security & Access Control

**US-4.1** — *As an organization owner, I want to invite my accountant with restricted access so they can view reports but cannot manage settings.*

| Criteria | Condition |
| :--- | :--- |
| **Given** | I am an OWNER of an organization |
| **When** | I invite a user with the ACCOUNTANT role |
| **Then** | They can view all financial data and reports, but cannot manage team members, delete data, or access billing |

**US-4.2** — *As any user, I expect that I will never see financial data belonging to another organization, even through API manipulation.*

| Criteria | Condition |
| :--- | :--- |
| **Given** | Two organizations exist with separate Tally data |
| **When** | User A attempts to access User B's data (including direct API calls with manipulated parameters) |
| **Then** | The request is rejected with 403 Forbidden, enforced by both application logic AND PostgreSQL Row-Level Security |

---

## 8. System Architecture Summary

### High-Level Architecture

```
╔══════════════════════════════════════════════════════════════════════════════════╗
║                          E-MUNSHI SYSTEM ARCHITECTURE                           ║
╠══════════════════════════════════════════════════════════════════════════════════╣
║                                                                                 ║
║  CUSTOMER PREMISES                     CLOUD (AWS Mumbai ap-south-1)           ║
║  ──────────────────                    ──────────────────────────────           ║
║                                                                                 ║
║  ┌──────────────────┐                  ┌──────────────────────────────────────┐ ║
║  │  TallyPrime /    │                  │  CDN (CloudFront) → React PWA       │ ║
║  │  Tally.ERP 9     │                  └──────────────────┬───────────────────┘ ║
║  │  (Port 9000)     │                                     │ HTTPS               ║
║  └────────┬─────────┘                  ┌──────────────────▼───────────────────┐ ║
║           │ HTTP XML (localhost)        │        FastAPI Backend               │ ║
║  ┌────────▼─────────┐  WSS/TLS         │  ┌────────────┐  ┌────────────────┐ │ ║
║  │  E-Munshi Local  │◄────────────────►│  │ Auth &     │  │ AI Orchestrator│ │ ║
║  │  Connector       │  (outbound only)  │  │ Session    │  │ (Intent →      │ │ ║
║  │  (Windows .exe)  │                   │  └────────────┘  │  Tool → SQL →  │ │ ║
║  │                  │                   │                   │  LLM explain)  │ │ ║
║  │  • TDL XML gen   │                   │  ┌────────────┐  └────────────────┘ │ ║
║  │  • Data parser   │                   │  │Deterministic│                     │ ║
║  │  • Delta sync    │                   │  │Financial    │                     │ ║
║  │  • BLOCK_WRITE=1 │                   │  │Engine       │                     │ ║
║  └──────────────────┘                   │  └────────────┘                      │ ║
║                                         │                                      │ ║
║  USER DEVICES                           │  ┌──────────────┐ ┌──────────────┐  │ ║
║  ┌──────────────────┐                   │  │ PostgreSQL   │ │ Redis        │  │ ║
║  │ Web Browser /    │  HTTPS            │  │ (RDS Mumbai) │ │ (Sessions,   │  │ ║
║  │ Mobile PWA       │◄────────────────►│  │ Multi-tenant │ │  Rate Limits)│  │ ║
║  └──────────────────┘                   │  │ RLS Enforced │ │              │  │ ║
║                                         │  └──────────────┘ └──────────────┘  │ ║
║                                         └──────────────────────────────────────┘ ║
╚══════════════════════════════════════════════════════════════════════════════════╝
```

### Trust Boundaries

| Zone | Components | Security Posture |
| :--- | :--- | :--- |
| **Zone 1: Customer Machine** | TallyPrime + E-Munshi Connector | Read-only; outbound-only; no inbound ports; encrypted local keystore |
| **Zone 2: E-Munshi Cloud** | API, DB, Redis, S3 | HTTPS/TLS 1.2+; RLS; JWT auth; rate limiting; audit logging |
| **Zone 3: External LLM** | Google Gemini API | Receives only structured JSON summaries — never raw financial data, PAN, GST, or party names in bulk |

---

## 9. Data Flow & Integration Design

### Tally Integration Protocol

E-Munshi connects to Tally using its built-in XML HTTP server on port 9000. This is a **standard, documented Tally feature** — not a hack or reverse-engineering approach.

```
REQUEST → POST http://localhost:9000
           Content-Type: text/xml;charset=utf-16
           Body: TDL (Tally Definition Language) XML Envelope

RESPONSE ← Content-Type: text/xml (utf-16le encoded)
            Body: Tally XML with requested data
```

### Data Sync Strategy

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  DATA SYNC LIFECYCLE                                                         │
│                                                                              │
│  PHASE 1: INITIAL SYNC (first connection)                                   │
│  ─────────────────────────────────────────                                  │
│  1. Fetch company list                                                      │
│  2. Fetch chart of accounts (ledgers + groups)                              │
│  3. Fetch current year vouchers (batches of 1,000)                          │
│  4. Fetch bill-wise outstanding (receivable + payable)                      │
│  5. Compress → encrypt → POST to cloud                                     │
│  6. Record sync_watermark = last ALTEREDID                                  │
│                                                                              │
│  PHASE 2: DELTA SYNC (every 15 minutes)                                    │
│  ───────────────────────────────────────                                    │
│  1. Query vouchers where ALTEREDID > last_watermark                         │
│  2. POST only changed records                                               │
│  3. Update sync_watermark                                                   │
│                                                                              │
│  PHASE 3: LIVE QUERIES (on-demand, selected reports)                        │
│  ─────────────────────────────────────────────────                          │
│  • Ledger Statement → live query via connector WebSocket                    │
│  • Trial Balance → live query when freshness < 5 minutes required           │
│                                                                              │
│  ERROR HANDLING                                                             │
│  • Tally offline → retry with backoff (5s, 10s, 30s, 5min, 30min)         │
│  • Network drop → resume from last watermark                                │
│  • Malformed XML → log, skip, never corrupt database                        │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Data Freshness Policy

| Data Type | Source | Staleness Tolerance | User Indication |
| :--- | :--- | :--- | :--- |
| Cash & Bank Balance | Delta sync (15 min) | 30 minutes | "As of HH:MM today" |
| Receivables / Outstanding | Delta sync (15 min) | 2 hours | "As of HH:MM today" |
| Trial Balance / P&L | Live from Tally | Must be live | "Fetched live from Tally" |
| Ledger Statement | Live from Tally | Must be live | "Fetched live from Tally" |
| Stock Summary | Delta sync (30 min) | 4 hours | "As of HH:MM today" |
| Master Data (Ledger Names) | On-demand refresh | 24 hours | Background refresh |

> **If Tally is offline**: E-Munshi serves the last synced data with a visible freshness warning. It **never** serves stale data silently.

---

## 10. AI & Financial Accuracy Strategy

### The Cardinal Rule

> **The LLM is an EXPLAINER, not a CALCULATOR.**
>
> Every financial figure displayed to a user comes from deterministic code execution (SQL queries + Python `Decimal(2)` arithmetic) against verified Tally data. The LLM only:
> 1. **Parses** the user's natural-language intent into structured parameters
> 2. **Routes** to the correct pre-built tool/function
> 3. **Explains** the deterministic result in friendly, readable language with source citations
>
> The LLM **NEVER** performs addition, subtraction, percentages, or any arithmetic operation. Period.

### Query Processing Pipeline

```
User Question → Intent Classification (LLM) → Parameter Guard → Deterministic 
SQL/Python Execution → Source-Cited Response Synthesis (LLM) → User
```

| Step | Performed By | Example |
| :--- | :--- | :--- |
| 1. Intent Classification | LLM (structured JSON output) | "Who owes me the most?" → `{ intent: QUERY_RECEIVABLES_AGING, sort: DESC }` |
| 2. Parameter Validation | Server-side code (no LLM) | Verify company access, validate date range, check intent allowlist |
| 3. Data Retrieval | SQL query (deterministic) | `SELECT party, SUM(outstanding) FROM bill_allocations WHERE tenant_id = :t ...` |
| 4. Computation | Python Decimal (deterministic) | Aging buckets, totals, percentages — all Python, zero LLM math |
| 5. Response Synthesis | LLM (grounded on data) | Takes structured JSON result → generates natural language with citations |

### Pilot Allowlisted Tools (10 Query Types)

| # | Tool | What It Returns |
| :--- | :--- | :--- |
| 1 | `get_cash_bank_balance` | Current cash + bank position |
| 2 | `get_profit_loss` | Revenue, expenses, net profit for period |
| 3 | `get_trial_balance` | Full trial balance with Dr/Cr totals |
| 4 | `get_outstanding_bills` | Party-wise receivable/payable bills |
| 5 | `get_receivables_aging` | Aging analysis: 0–30, 31–60, 61–90, 90+ days |
| 6 | `get_ledger_statement` | Full ledger account statement with running balance |
| 7 | `get_stock_summary` | Item-wise stock quantities and values |
| 8 | `get_top_customers` | Ranked customers by revenue or outstanding |
| 9 | `get_expense_analysis` | Expense breakdown by group/category |
| 10 | `compare_periods` | Period-over-period comparison (sales, profit, expenses) |

### Anti-Hallucination Safeguards

| Safeguard | Implementation |
| :--- | :--- |
| **No LLM Math** | All arithmetic performed in Python `Decimal(2)` — LLM receives pre-computed results as strings |
| **Source Citation** | Every response includes: report name, company, date range, data freshness timestamp |
| **Number as Strings** | Amounts passed to LLM as JSON strings (`"1245000"` not `1245000.0`) to prevent reformatting |
| **Intent Allowlist** | Only 10 pre-approved query types; unsupported queries return structured refusal |
| **Prompt Injection Defense** | Tally ledger names, narrations treated as untrusted input; never injected raw into prompts |
| **Backend Validation** | If LLM generates a figure not present in the structured data, response is rejected |

---

## 11. Security & Compliance Requirements

### Security Architecture (7 Layers)

| Layer | Controls |
| :--- | :--- |
| **1. Transport** | TLS 1.2+ on all endpoints; WSS for connector; HSTS headers; Secure + HttpOnly cookies |
| **2. Authentication** | JWT (15-min access, 7-day refresh with rotation); Google OAuth 2.0 PKCE; one-time pairing tokens |
| **3. Authorization** | Role-based (Owner/Accountant/Viewer); tenant_id extracted server-side from JWT — client cannot inject |
| **4. Input Validation** | Pydantic v2 schemas on all inputs; date range validation; intent allowlist; SQL injection prevention |
| **5. Data Protection** | AES-256 at rest (RDS); S3 pre-signed URLs (15-min TTL); PAN/GST masked in logs; no raw data to LLM |
| **6. Rate Limiting** | Redis sliding window: 50 queries/user/hour; 500 API calls/org/hour; 1 sync/5 min/company |
| **7. Audit Logging** | Every query, report fetch, sync event, and login logged with full context; 90-day retention |

### Data Residency

All data stored and processed within **AWS Mumbai (ap-south-1)**. No financial data leaves India. LLM API calls send only structured summaries (never raw transaction data) to the provider's API endpoint.

### Compliance Considerations

| Area | Status |
| :--- | :--- |
| Data residency (India) | ✅ Enforced — AWS Mumbai |
| Personal data handling | ✅ PAN/GST masked in logs; not sent to LLM |
| Data retention policy | ✅ Documented — 24 months financial data; 12 months chat history |
| Right to data deletion | 🔶 Planned — API to purge all org data on account closure |
| DPDP Act 2023 compliance | 🔶 Review pending — consent management and data principal rights |

---

## 12. Technology Stack

| Layer | Technology | Rationale |
| :--- | :--- | :--- |
| **Frontend** | React 19 + Vite + TypeScript | Fastest build tooling; huge ecosystem; excellent developer productivity |
| **Styling** | Vanilla CSS / CSS Modules | Maximum control; no framework dependency |
| **Charts** | Recharts / Chart.js | Lightweight; great for financial data visualization |
| **Data Fetching** | TanStack Query | Caching, refetching, optimistic updates — ideal for frequently-changing financial data |
| **Backend** | Python 3.12 + FastAPI | Best-in-class AI ecosystem; Pydantic for financial data validation; async-native |
| **ORM** | SQLAlchemy 2.x (async) + Alembic | Mature, production-proven; migration management |
| **Database** | PostgreSQL 16 (AWS RDS / Supabase Mumbai) | ACID guarantees; Row-Level Security; JSONB for flexible schemas |
| **Caching** | Redis 7 (Upstash / ElastiCache) | Session tokens, rate limiting, sync job queuing |
| **AI/LLM** | Google Gemini 2.0 Flash via LiteLLM | 50% cheaper than GPT-4o-mini; 1M context window; strong Indian language support; provider-agnostic wrapper |
| **Auth** | Supabase Auth (JWT + refresh) | Email + Google OAuth; India-hosted; generous free tier |
| **Connector** | Node.js (TypeScript), packaged as single `.exe` | Reuses proven TDL templates from `tally-mcp-server` (ISC license — commercially free) |
| **File Storage** | AWS S3 (Mumbai) | Pre-signed URLs for exports; Indian data residency |
| **CI/CD** | GitHub Actions | Free for private repos; integrates with AWS deployment |
| **Hosting** | AWS Lightsail / EC2 (Mumbai) + CloudFront | Predictable cost; Mumbai region; easy scaling path |
| **Monitoring** | Sentry (errors) + Grafana Cloud (metrics) | Generous free tiers for pilot phase |

---

## 13. UX/UI Requirements

### Design Principles

| Principle | Implementation |
| :--- | :--- |
| **Data Trust** | Every number shows its source and freshness — users should never wonder "is this accurate?" |
| **Financial Literacy** | Use plain language labels (not accounting jargon); color-code good/bad metrics |
| **Speed** | Perceived performance via skeleton loaders; SSE streaming for chat; optimistic UI updates |
| **Accessibility** | WCAG 2.1 AA compliant; keyboard navigation; sufficient color contrast |
| **Mobile-First** | Responsive PWA; critical metrics readable on a 5-inch phone screen |

### Key Screens

#### Screen 1: Dashboard
```
┌──────────────────────────────────────────────────────────────────┐
│  🏢 Company: Acme Corp ▼        ●LIVE (synced 14:23 today)     │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌─────────────────┐  ┌──────────────────────────────────────┐  │
│  │ 💰 Cash & Bank  │  │ 📈 Sales This Month                 │  │
│  │   ₹18.4 Lakhs   │  │   ₹42.1L  (▲12% vs last month)     │  │
│  └─────────────────┘  └──────────────────────────────────────┘  │
│                                                                  │
│  ┌─────────────────────┐  ┌──────────────────────────────────┐  │
│  │ Top 5 Debtors       │  │ ⚠ Overdue Summary               │  │
│  │ ████████ Sunrise     │  │  0-30 days:  ₹8.2L  (12 bills)  │  │
│  │ ██████ Galaxy        │  │  31-60 days: ₹3.1L  (5 bills)   │  │
│  │ ████ Prism           │  │  61-90 days: ₹1.4L  (3 bills)   │  │
│  │ ███ Nova             │  │  90+ days:   ₹6.8L  (8 bills) 🔴│  │
│  │ ██ Star              │  │                                   │  │
│  └─────────────────────┘  └──────────────────────────────────┘  │
│                                                                  │
│  Quick Ask: [Show P&L] [Who owes me?] [Cash position] [More…]  │
└──────────────────────────────────────────────────────────────────┘
```

#### Screen 2: AI Chat
```
┌──────────────────────────────────────────────────────────────────┐
│  E-Munshi AI Chat               🏢 Acme Corp ▼                  │
├────────────────┬─────────────────────────────────────────────────┤
│ ≡ Conversations│                                                 │
│                │  🧑 Who owes me the most money?                │
│ • Today        │                                                 │
│   - Cash flow  │  🤖 Based on your Bills Outstanding as of      │
│   - Debtors    │     Oct 26, 2026 (synced 14:23 today):        │
│                │                                                 │
│ • Yesterday    │     1. Sunrise Traders — ₹8,42,000 (67 days)   │
│   - P&L query  │     2. Galaxy Enterprises — ₹5,18,000 (45 d)  │
│                │     3. Prism Industries — ₹3,91,000 (23 days)  │
│                │                                                 │
│                │     📋 Source: Bills Outstanding (Receivable)   │
│                │     🕐 Data as of: 14:23 today                  │
│                │                                                 │
│                │     Try: [Show aging details] [Export to Excel] │
│                │          [Send payment reminder draft]          │
│                │                                                 │
│                │  ┌──────────────────────────────────────┐      │
│                │  │ Type your question…                   │ ➤   │
│                │  └──────────────────────────────────────┘      │
└────────────────┴─────────────────────────────────────────────────┘
```

---

## 14. Release Plan & Milestones

### 30-Day Sprint Plan

```
═══════════════════════════════════════════════════════════════════════════
 WEEK 1 (Days 1–7): Foundation & Tally Connector PoC
═══════════════════════════════════════════════════════════════════════════
 • Environment setup: GitHub repo, FastAPI skeleton, React+Vite scaffold
 • PostgreSQL schema: organizations, users, memberships, connectors
 • Tally connector: extract TDL templates from tally-mcp-server
 • Delta sync logic with ALTEREDID watermark tracking
 • Cloud ingestion API + connector pairing flow
 • First deploy to AWS Mumbai

 EXIT: User can login → pair connector → see synced data in DB

═══════════════════════════════════════════════════════════════════════════
 WEEK 2 (Days 8–14): Financial Engine & Dashboard
═══════════════════════════════════════════════════════════════════════════
 • Deterministic financial engine: aging, P&L, trial balance, cash flow
 • Report API endpoints with data freshness metadata
 • Frontend dashboard: cash card, sales card, debtors chart, aging summary
 • Unit tests: engine output vs. manually verified Tally reports

 EXIT: Dashboard figures match Tally figures for test company

═══════════════════════════════════════════════════════════════════════════
 WEEK 3 (Days 15–21): AI Chat & Exports
═══════════════════════════════════════════════════════════════════════════
 • Gemini integration via LiteLLM
 • Intent classification + tool allowlist + parameter guard
 • SSE streaming chat interface
 • XLSX/PDF exports with S3 pre-signed URLs
 • Rate limiting + error handling + edge cases

 EXIT: 10 sample questions return verified, source-cited answers

═══════════════════════════════════════════════════════════════════════════
 WEEK 4 (Days 22–30): Security, Testing & Pilot Launch
═══════════════════════════════════════════════════════════════════════════
 • Security audit: cross-tenant, JWT, injection testing
 • Connector packaging: single .exe for Windows
 • Pilot onboarding: 2–3 real users
 • Polish: loading states, animations, documentation

 EXIT: 3+ real users using the product with no critical data issues
```

### Milestone Acceptance Criteria

| Milestone | Day | Gate |
| :--- | :--- | :--- |
| **M1** — Tally Extraction PoC | Day 4 | Extract 5 report types from live Tally; totals match |
| **M2** — Cloud Sync Working | Day 7 | Login → pair → sync → verify data flow end-to-end |
| **M3** — Financial Engine Verified | Day 14 | Dashboard figures = Tally figures for 3 test periods |
| **M4** — AI Chat Operational | Day 21 | 10 sample queries answered with source citations |
| **M5** — Security Pass | Day 23 | Zero cross-tenant access; complete audit logs |
| **M6** — Pilot Launch | Day 30 | 3+ real users; no critical bugs; data accuracy confirmed |

---

## 15. Budget & Cost Projections

### Monthly Infrastructure Cost (Pilot)

| Service | Provider | Monthly Cost (₹) |
| :--- | :--- | :--- |
| API Server | AWS Lightsail (2 vCPU, 4GB, Mumbai) | ₹1,650 |
| Database | Supabase Pro (PostgreSQL, Mumbai) | ₹2,100 |
| Redis | Upstash (Serverless) | ₹0–400 |
| Frontend CDN | AWS CloudFront + S3 | ₹200 |
| LLM (Gemini Flash) | Google Cloud (~15k queries/mo) | ₹1,200 |
| Object Storage | AWS S3 (Mumbai) | ₹150 |
| Email | Resend / Brevo (Free tier) | ₹0 |
| Monitoring | Sentry + Grafana Cloud (Free tier) | ₹0 |
| Domain | emunshi.in | ₹67 |
| **TOTAL** | | **~₹5,770/month** |

### 3-Month Projected Total

| Category | 3-Month Cost (₹) |
| :--- | :--- |
| Cloud infrastructure | ₹17,310 |
| LLM API (scaled to 75k queries) | ₹600 |
| Domain + Email setup | ₹2,500 |
| AI development tooling | ₹7,500 |
| **GRAND TOTAL** | **₹27,910** |

> **Budget Assessment**: Full pilot deliverable for under ₹30,000 over 3 months. Well within a ₹50K–₹1L budget, leaving headroom for marketing, user onboarding, and security testing.

### Proposed Pricing Model

| Plan | Price | Includes |
| :--- | :--- | :--- |
| **Starter** | ₹399/month or ₹3,999/year | 1 user, 1 company, 500 queries/month |
| **Business** | ₹9,999/year | 5 users, 5 companies, unlimited queries |
| **CA / Teams** | ₹18,000/year | 10 users, 20 companies, white-label option, priority support |
| **Free Trial** | 14 days, no card required | Full Business tier features |

---

## 16. Competitive Positioning

### E-Munshi vs. Riko AI

| Capability | Riko AI | E-Munshi (Pilot v1) | E-Munshi Advantage |
| :--- | :---: | :---: | :--- |
| AI Chat with Tally Data | ✅ | ✅ | Parity |
| P&L, Trial Balance, Balance Sheet | ✅ | ✅ | Parity |
| Receivables/Payables Aging | ✅ | ✅ | Parity |
| Cash & Bank Position | ✅ | ✅ | Parity |
| Multi-Company Support | ✅ | ✅ | Parity |
| Source-Cited Answers | ✅ | ✅ | Parity |
| Data Freshness Indicators | Partial | ✅ Full | **E-Munshi leads** — every metric timestamped |
| PostgreSQL RLS Isolation | Unknown | ✅ | **E-Munshi leads** — defense-in-depth |
| Transparent AI (no LLM math) | Unknown | ✅ | **E-Munshi leads** — documented & auditable |
| GST Reconciliation | ✅ | ❌ v2 | Riko leads (temporarily) |
| WhatsApp Bot | ✅ | ❌ v2 | Riko leads (temporarily) |
| Write to Tally | ✅ (paid) | ❌ v2 | Riko leads (temporarily) |
| **Entry Price** | ₹5,000/year | ₹3,999/year | **E-Munshi: 20% cheaper** |
| **Free Trial** | 7 days | 14 days | **E-Munshi: 2x longer trial** |

### Strategic Differentiation

1. **Price undercut**: 20% cheaper entry point with longer free trial
2. **CA-first positioning**: Multi-client management, role-based access, future white-label
3. **Transparency & trust**: Every answer shows its data source, timestamp, and computation method
4. **Security as a feature**: PostgreSQL RLS, no raw data to LLM — documented and auditable

---

## 17. Risks, Dependencies & Assumptions

### Risk Register

| # | Risk | Probability | Impact | Mitigation |
| :--- | :--- | :---: | :---: | :--- |
| R1 | Tally port blocked by antivirus/Windows Defender | HIGH | HIGH | Test on 3+ Windows setups; document allow-list; connector diagnostic tool |
| R2 | Large Tally databases (100k+ vouchers) cause slow initial sync | HIGH | MEDIUM | Batch sync (1k/request); progress indicator; set expectations |
| R3 | Single developer cannot deliver full scope in 30 days | HIGH | HIGH | Explicit scope reduction (see §4); AI coding tools accelerate delivery |
| R4 | LLM provides confidently wrong financial commentary | MEDIUM | HIGH | Zero LLM math; source citations; backend validation layer |
| R5 | Customer runs Tally on cloud VM with restricted port access | MEDIUM | HIGH | Document requirements; connector must run on same machine as Tally |
| R6 | Tally Educational Edition gives incorrect data | MEDIUM | HIGH | Detect and reject at connector startup |
| R7 | Prompt injection via malicious Tally ledger names | MEDIUM | HIGH | Ledger names as untrusted input; escaped before prompt injection |
| R8 | Gemini API pricing change or outage | LOW | MEDIUM | LiteLLM wrapper — switch provider in 2 config lines |
| R9 | Data residency regulatory requirements | LOW | HIGH | AWS Mumbai only; no data leaves India; documented privacy policy |

### Key Dependencies

| Dependency | Owner | Status |
| :--- | :--- | :--- |
| TallyPrime must be running and configured as server on port 9000 | Customer | Requires setup guidance |
| AWS Mumbai region availability | AWS | Stable; multi-AZ for production |
| Google Gemini 2.0 Flash API access | Google Cloud | Available; free tier + paid |
| `tally-mcp-server` TDL templates (ISC license) | Open Source | Verified — commercially free |
| Pilot customer(s) with live Tally data willing to test | Business team | **Must be secured by Day 15** |

### Assumptions

1. Pilot customers use TallyPrime 3.x or later (or Tally.ERP 9 Release 6+)
2. Tally is installed on a local Windows PC or LAN server (not cloud-only TSS without port access)
3. Customer can install the connector .exe on the Tally machine (no enterprise IT lockdown)
4. Internet connectivity is available on the Tally machine (for outbound sync)
5. Pilot data volume is under 500,000 vouchers per company

---

## 18. Open Questions & Pre-Development Blockers

> **These questions MUST be answered before or during the first 3 days of development.**

| # | Question | Why It Matters | Priority |
| :--- | :--- | :--- | :---: |
| **Q1** 🔴 | Which Tally version(s) do pilot customers use? | TDL templates differ between versions; some bill-wise fields missing in older ERP 9 | BLOCKING |
| **Q2** 🔴 | Is Tally running on a local PC, LAN server, or cloud VM? | Cloud/VM may have port access restrictions that break the connector | BLOCKING |
| **Q3** 🔴 | Approximate voucher volume per company? | Affects sync strategy, batching, and user experience expectations | BLOCKING |
| **Q4** 🔴 | Single-company or multi-company Tally setups? | Multi-company needs company selection UI from Day 1 | BLOCKING |
| **Q5** 🔴 | Which Tally reports serve as ground truth for accuracy validation? | Cannot verify financial accuracy without agreed reference outputs | BLOCKING |
| Q6 | Who will install the connector — business owner or their CA? | Affects installer UX (technical vs. non-technical) | HIGH |
| Q7 | Chat history retention policy — how long? | Privacy and data retention implications | HIGH |
| Q8 | White-label option needed for CA firms at launch? | Architecture impact on domain routing and branding | HIGH |
| Q9 | Any specific customer Data Processing Agreement (DPA) requirements? | Legal compliance before onboarding enterprise customers | HIGH |
| Q10 | Existing frontend codebase to integrate, or building from scratch? | Significantly changes Week 1 timeline | MEDIUM |
| Q11 | Write operations needed for any pilot use case, or strictly deferred? | Write access changes entire security model and review scope | MEDIUM |
| Q12 | Which domains are available? (emunshi.in, .com, getmunshi.in) | Register before competitors | MEDIUM |
| Q13 | Connector auto-update: silent or user-prompted? | Enterprise customers may require manual update approval | LOW |

---

## 19. Success Metrics & KPIs

### Pilot Success Criteria (Day 30)

| Metric | Target | Measurement |
| :--- | :--- | :--- |
| **Pilot users onboarded** | ≥ 3 real users (business owners or CAs) | Active accounts with connected Tally |
| **Financial accuracy** | 100% match with Tally reports | Trial Balance, P&L, Outstanding Bills compared for 3 test periods |
| **Data sync reliability** | ≥ 95% sync success rate | Sync run logs — successful/failed ratio |
| **Chat accuracy** | 100% of supported queries return correct, source-cited answers | Manual QA against 20 test queries |
| **Response time** | < 5 seconds for 95% of chat queries | Grafana P95 latency dashboard |
| **Security** | Zero cross-tenant data access | Automated security test suite passes |
| **Uptime** | ≥ 99% during pilot month | Uptime monitoring |
| **Critical bugs** | Zero unresolved critical bugs | Issue tracker |

### Post-Pilot Business KPIs (Months 2–6)

| Metric | Target |
| :--- | :--- |
| Free trial sign-ups | 100+ in first 3 months |
| Trial → paid conversion rate | ≥ 15% |
| Monthly recurring revenue (MRR) | ₹50,000+ by Month 6 |
| Daily active users | ≥ 30 |
| Average queries per user per day | ≥ 5 |
| Net Promoter Score (NPS) | ≥ 40 |
| Churn rate (monthly) | < 5% |

---

## 20. Future Roadmap (Post-Pilot)

### v2 Features (Months 2–4)

| Feature | Description | Business Value |
| :--- | :--- | :--- |
| **WhatsApp Business Bot** | Conversational Tally queries via WhatsApp; payment reminder templates | Reach non-tech-savvy owners on their preferred channel |
| **GST Reconciliation** | Match GSTR-2A/2B with Tally purchase data; flag mismatches | Solve a major CA pain point; high willingness to pay |
| **Monthly MIS Auto-Generation** | Scheduled report packs (P&L, BS, Cash Flow, Aging) emailed to stakeholders | Replaces manual 2-day process for CAs |
| **Write to Tally (with Approval)** | Create journal entries, payment receipts via E-Munshi with maker-checker workflow | Competitive parity with Riko AI paid tier |
| **Bank Reconciliation** | Import bank statements; auto-match with Tally entries | Major time-saver for accountants |

### v3 Features (Months 5–8)

| Feature | Description |
| :--- | :--- |
| **Mobile Native App** | Android + iOS app for business owners |
| **Multi-Language UI** | Hindi, Gujarati, Marathi interfaces |
| **Predictive Analytics** | Cash flow forecasting, seasonal trend prediction |
| **Custom Report Builder** | Drag-and-drop report designer |
| **API Platform** | Public API for third-party integrations |
| **White-Label for CA Firms** | Custom domain, branding, and client management portal |

---

## 21. Glossary

| Term | Definition |
| :--- | :--- |
| **Tally** | India's dominant accounting software (TallyPrime / Tally.ERP 9), used by 7+ million businesses |
| **TDL** | Tally Definition Language — XML-based query language for extracting data from Tally |
| **Port 9000** | Tally's built-in HTTP XML server port, used for programmatic data access |
| **ALTEREDID** | Tally's internal sequence number that increments when records are created or modified — used for delta sync |
| **RLS** | Row-Level Security — a PostgreSQL feature that enforces data access policies at the database level |
| **LLM** | Large Language Model — AI model (e.g., Google Gemini) used for natural language understanding |
| **SSE** | Server-Sent Events — HTTP streaming protocol for real-time updates |
| **JWT** | JSON Web Token — industry-standard authentication token format |
| **Delta Sync** | Incremental data synchronization — only transfers records changed since last sync |
| **MSME** | Micro, Small, and Medium Enterprises — India's largest business segment |
| **CA** | Chartered Accountant — a licensed accounting professional in India |
| **PWA** | Progressive Web Application — a website that can be installed on mobile devices and work offline |
| **MIS** | Management Information System — periodic financial reports for business decision-making |
| **Dr/Cr** | Debit/Credit — fundamental accounting concepts; debits increase assets, credits increase liabilities |
| **GSTR-2A/2B** | GST return forms auto-populated by the government based on supplier filings |
| **DPAPI** | Windows Data Protection API — used for encrypting local secrets on Windows |
| **PAN** | Permanent Account Number — India's tax identification number |
| **GST/GSTN** | Goods and Services Tax / GST Network — India's indirect tax system |

---

## 22. Appendices

### Appendix A: Supported Tally Versions

| Version | Support Level | Notes |
| :--- | :--- | :--- |
| TallyPrime 3.x / 4.x / 5.x | ✅ Fully Supported | Primary target |
| TallyPrime 2.x | ✅ Supported | XML port stable |
| Tally.ERP 9 (Release 6+) | ✅ Supported | Widely deployed |
| Tally.ERP 9 (< Release 6) | ⚠ Limited | Missing bill-wise fields |
| Tally Educational Edition | ❌ Not Supported | Date restrictions cause invalid data |
| Tally on Cloud / TSS | ⚠ Requires Testing | Port 9000 accessibility must be verified |

### Appendix B: Data Model (Entity Relationship)

```
organizations ──┐
                 ├──► memberships ◄── users
                 │
                 ├──► connectors
                 │
                 └──► accounting_companies ──┬──► ledgers
                                             ├──► vouchers
                                             ├──► bill_allocations
                                             ├──► sync_runs
                                             └──► chat_sessions ──► chat_messages

                      audit_events (cross-cutting — logs all actions)
```

### Appendix C: API Endpoint Summary

```
Auth:      POST /auth/login, /auth/google, /auth/refresh, DELETE /auth/logout
User:      GET /me
Orgs:      POST /organizations, GET /organizations/:id
Companies: GET /companies
Connector: POST /connectors/pair-init, GET /connectors/status
Sync:      POST /sync/delta, GET /sync/runs
Reports:   GET /reports/trial-balance, /profit-loss, /balance-sheet,
           /outstanding-bills, /ledger-statement, /stock-summary
Chat:      POST /chat/sessions, POST /chat/sessions/:id/messages (SSE),
           GET /chat/sessions
Files:     GET /files/:file_id
Audit:     GET /audit/events
```

### Appendix D: Pilot Release Checklist

- [ ] Cross-tenant data access test passed
- [ ] JWT token rotation and expiry verified
- [ ] SQL injection attempted and blocked on all inputs
- [ ] Prompt injection test passed (malicious ledger names)
- [ ] BLOCK_WRITE=1 confirmed on connector
- [ ] Trial Balance totals match Tally (3 test periods)
- [ ] P&L net profit matches Tally (3 test periods)
- [ ] Receivables total matches Tally (3 dates)
- [ ] Cash balance matches Tally Balance Sheet
- [ ] Aging buckets manually verified (10 bills)
- [ ] Connector tested on 2 clean Windows machines
- [ ] Tally restart recovery tested (< 60 seconds)
- [ ] Network drop recovery tested (no duplicates)
- [ ] 50,000+ voucher company synced without Tally freeze
- [ ] Production monitoring active (Sentry + uptime check)
- [ ] Database backups enabled (7-day retention)
- [ ] Secrets not in source code (environment variables only)
- [ ] Rollback procedure documented and tested

### Appendix E: Reference Materials

| Resource | URL | Purpose |
| :--- | :--- | :--- |
| Riko AI (Competitor) | https://rikoai.in | Feature benchmark and UX reference |
| Tally MCP Server (Open Source) | https://github.com/dhananjay1405/tally-mcp-server | TDL template source; ISC license |
| E-Munshi Architecture Document | Internal | Detailed technical architecture (companion to this PRD) |

---

## 23. Approval & Sign-Off

| Role | Name | Date | Signature |
| :--- | :--- | :--- | :--- |
| **Product Owner / Client** | | | ☐ Approved |
| **Engineering Lead** | | | ☐ Approved |
| **Business Stakeholder** | | | ☐ Approved |

---

> **Next Steps After Approval:**
> 1. Resolve all 🔴 BLOCKING questions (§18, Q1–Q5) within 48 hours
> 2. Confirm pilot customer availability and Tally setup details
> 3. Commence Week 1 sprint on agreed start date
> 4. First milestone review (M1 — Tally Extraction PoC) on Day 4

---

*Document prepared by: E-Munshi Engineering Team*
*Classification: Confidential — Client Review*
*Version: 1.0 | October 26, 2026*
*Companion document: [E-Munshi Product Architecture Document](./E-Munshi_Product_Architecture_Document.md)*
