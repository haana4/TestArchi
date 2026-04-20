# Platform Engineering Capability Architecture — Complete Reference Model

---

## Table of Contents

1. [Architecture Overview](#1-architecture-overview)
2. [Layer 1: Strategic & Agile Planning](#2-layer-1-strategic--agile-planning)
3. [Layer 2: Engineering & Product Analytics](#3-layer-2-engineering--product-analytics)
4. [Layer 3: Developer Plane](#4-layer-3-developer-plane)
5. [Layer 4: Platform Integration & Delivery Services](#5-layer-4-platform-integration--delivery-services)
6. [Layer 5: Application & Portfolio Management](#6-layer-5-application--portfolio-management)
7. [Layer 6: Service Management & Incident Management](#7-layer-6-service-management--incident-management)
8. [Layer 7: Observability & Monitoring](#8-layer-7-observability--monitoring)
9. [Layer 8 (Cross-Cutting): Knowledge Management](#9-layer-8-cross-cutting-knowledge-management)
10. [Layer 9 (Cross-Cutting): Open Source Governance & Enablers](#10-layer-9-cross-cutting-open-source-governance--enablers)
11. [Layer 10 (Cross-Cutting): FinOps](#11-layer-10-cross-cutting-finops)
12. [Layer 11 (Cross-Cutting): Security Services](#12-layer-11-cross-cutting-security-services)
13. [Layer 12 (Cross-Cutting): Infrastructure & Resource Services](#13-layer-12-cross-cutting-infrastructure--resource-services)
14. [Feedback Flow Model](#14-feedback-flow-model)
15. [Three Catalogs — How They Differ](#15-three-catalogs--how-they-differ)
16. [Layer Dependency Map](#16-layer-dependency-map)
17. [Product Ownership Structure](#17-product-ownership-structure)
18. [Mission Model: Secrets & Dependency Management Prioritisation](#18-mission-model-secrets--dependency-management-prioritisation)
19. [Budget Allocation Model](#19-budget-allocation-model)
20. [Complete Layer Inventory Summary](#20-complete-layer-inventory-summary)

---

## 1. Architecture Overview

```
                        FEEDBACK DESTINATIONS

              ┌──────────────────────────────────────────────────────────┐
              │                                                          │
              ▼                                                          ▼
┌──────────────────────────┐                          ┌──────────────────────────┐
│ PLATFORM PRODUCT         │                          │ DOMAIN PRODUCT           │
│ MANAGEMENT               │                          │ TEAMS                    │
│ (Head of Product, SPOs)  │                          │ (Payments, Lending,      │
│                          │                          │  CX, Merchant, etc.)     │
└────────────┬─────────────┘                          └────────────┬─────────────┘
             │                                                     │
             │  investment decisions feed into                     │
             ▼                                                     ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│                      STRATEGIC & AGILE PLANNING                              │
│                                                                              │
│  ┌──────────────────────┐  ┌──────────────────────┐  ┌────────────────────┐  │
│  │ Enterprise Planning  │──▶ Digital Product      │──▶ Technical          │  │
│  │                      │  │ Planning             │  │ Planning           │  │
│  └──────────────────────┘  └──────────────────────┘  └────────────────────┘  │
└──────────────────────────────┬───────────────────────────────────────────────┘
                               │ demand signals flow down
                               ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│                    ENGINEERING & PRODUCT ANALYTICS                            │
│                                                                              │
│  ┌─────────────────────────────────────────────────────────────────────────┐  │
│  │                 SHARED ANALYTICS INFRASTRUCTURE                        │  │
│  │  ┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐       │  │
│  │  │ Data Ingestion   │ │ Analytics Data   │ │ Dashboards,      │       │  │
│  │  │ & Pipelines      │ │ Platform & APIs  │ │ Reporting &      │       │  │
│  │  │                  │ │                  │ │ Self-Service BI  │       │  │
│  │  └──────────────────┘ └──────────────────┘ └──────────────────┘       │  │
│  └─────────────────────────────────────────────────────────────────────────┘  │
│                                                                              │
│  ┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐              │
│  │ Delivery &       │ │ Product & Value  │ │ Developer        │              │
│  │ Engineering      │ │ Analytics        │ │ Productivity &   │              │
│  │ Analytics        │ │                  │ │ Experience       │              │
│  └──────────────────┘ └──────────────────┘ └──────────────────┘              │
│  ┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐              │
│  │ Platform         │ │ Quality &        │ │ Executive        │              │
│  │ Analytics        │ │ Security         │ │ Dashboards &     │              │
│  │ (self-analytics) │ │ Analytics        │ │ Reporting        │              │
│  └──────────────────┘ └──────────────────┘ └──────────────────┘              │
└──────────────────────────────┬───────────────────────────────────────────────┘
                               │ insights inform
                               ▼
                        ◀─────────── SOFTWARE DEVELOPMENT LIFECYCLE ───────────▶

                         PLAN &        BUILD &        DELIVER &       OPERATE &
                         DESIGN        TEST           DEPLOY          RUN

┌────────────────────┐  ┌─────────┐  ┌──────────┐   ┌──────────┐   ┌──────────┐
│                    │  │Plan &   │  │Build &   │   │Deliver & │   │Operate & │
│   IDE              │  │Design   │  │Test      │   │Deploy    │   │Run       │
│                    │  │Capabil- │  │Capabil-  │   │Capabil-  │   │Capabil-  │
│   Agentic          │  │ities   │  │ities     │   │ities     │   │ities     │
│   Development ─────┼──│         │──│          │───│          │───│          │
│   Platform         │  │         │  │          │   │          │   │          │
│                    │  │         │  │          │   │          │   │          │
│   Fast Prototyping │  │         │  │          │   │          │   │          │
│   Capabilities     │  │         │  │          │   │          │   │          │
│                    │  │         │  │          │   │          │   │          │
│  DEVELOPER PLANE   │  └─────────┘  └──────────┘   └──────────┘   └──────────┘
└────────────────────┘       │            │               │              │
                             └────────────┴───────────────┴──────────────┘
                                          │
                                    consumes & orchestrates
                                          │
┌─────────────────────────────────────────▼────────────────────────────────────┐
│               PLATFORM INTEGRATION & DELIVERY SERVICES                       │
│                                                                              │
│  ┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐              │
│  │ API & Service    │ │ Data & Event     │ │ Delivery &       │              │
│  │ Integration      │ │ Services         │ │ Runtime Orch.    │              │
│  └──────────────────┘ └──────────────────┘ └──────────────────┘              │
│  ┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐              │
│  │ Developer Self-  │ │ Configuration &  │ │ Platform         │              │
│  │ Service          │ │ Secrets Mgmt     │ │ Extensibility    │              │
│  │ Interfaces       │ │                  │ │                  │              │
│  └──────────────────┘ └──────────────────┘ └──────────────────┘              │
│  ┌──────────────────┐                                                        │
│  │ Sandbox & Rapid  │                                                        │
│  │ Provisioning     │                                                        │
│  └──────────────────┘                                                        │
└──────────────────────────────┬───────────────────────────────────────────────┘
                               │ registered in & governed by
                               │
┌──────────────────────────────▼───────────────────────────────────────────────┐
│               APPLICATION & PORTFOLIO MANAGEMENT                             │
│                                                                              │
│  ┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐              │
│  │ Software System  │ │ Digital Product  │ │ Application      │              │
│  │ Catalog          │ │ Catalog          │ │ Lifecycle Mgmt   │              │
│  └──────────────────┘ └──────────────────┘ └──────────────────┘              │
│  ┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐              │
│  │ Dependency &     │ │ Standards &      │ │ Technology       │              │
│  │ Topology Mgmt    │ │ Governance       │ │ Audit Service    │              │
│  └──────────────────┘ └──────────────────┘ └──────────────────┘              │
└──────────────────────────────┬───────────────────────────────────────────────┘
                               │ operational lifecycle managed by
                               │
┌──────────────────────────────▼───────────────────────────────────────────────┐
│                SERVICE MANAGEMENT & INCIDENT MANAGEMENT                       │
│                                                                              │
│  ┌──────────────────┐ ┌────────────────┐ ┌───────────────┐ ┌─────────────┐   │
│  │ Service Catalog  │ │ Change Mgmt &  │ │ Incident      │ │ On-Call,    │   │
│  │ & Ownership      │ │ Approval Flows │ │ Detection,    │ │ Escalation &│   │
│  │                  │ │                │ │ Triage &      │ │ Runbook     │   │
│  │                  │ │                │ │ Resolution    │ │ Automation  │   │
│  └──────────────────┘ └────────────────┘ └───────────────┘ └─────────────┘   │
└──────────────────────────────┬───────────────────────────────────────────────┘
                               │ informed by
┌──────────────────────────────▼───────────────────────────────────────────────┐
│                       OBSERVABILITY & MONITORING                             │
│                                                                              │
│  ┌──────────┐ ┌──────────┐ ┌───────────┐ ┌───────────┐ ┌─────────┐          │
│  │ Metrics  │ │ Logging  │ │ Tracing   │ │ Alerting  │ │ SLO/SLI │          │
│  │          │ │          │ │           │ │ & AIOps   │ │ Mgmt    │          │
│  └──────────┘ └──────────┘ └───────────┘ └───────────┘ └─────────┘          │
└──────────────────────────────────────────────────────────────────────────────┘

┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
│                                                          CROSS-CUTTING       │
│                                                                              │
│  ┌─────────────────────────────────────────────────────────────────────────┐  │
│  │                     KNOWLEDGE MANAGEMENT                               │  │
│  └─────────────────────────────────────────────────────────────────────────┘  │
│  ┌─────────────────────────────────────────────────────────────────────────┐  │
│  │                  OPEN SOURCE GOVERNANCE & ENABLERS                     │  │
│  └─────────────────────────────────────────────────────────────────────────┘  │
│  ┌─────────────────────────────────────────────────────────────────────────┐  │
│  │                            FINOPS                                      │  │
│  └─────────────────────────────────────────────────────────────────────────┘  │
│  ┌─────────────────────────────────────────────────────────────────────────┐  │
│  │                        SECURITY SERVICES                               │  │
│  └─────────────────────────────────────────────────────────────────────────┘  │
│  ┌─────────────────────────────────────────────────────────────────────────┐  │
│  │                  INFRASTRUCTURE & RESOURCE SERVICES                     │  │
│  └─────────────────────────────────────────────────────────────────────────┘  │
└ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘
```

---

## 2. Layer 1: Strategic & Agile Planning

*The demand signal layer — translates organisational strategy into executable work across the SDLC.*

### 1.1 Enterprise Planning

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Strategic OKRs & Themes** | • OKR definition & cascading • Strategic theme management • Key result tracking & scoring • Cross-portfolio alignment reviews | Atlassian Focus, Workboard, Gtmhub, Perdoo |
| **Portfolio Investment & Funding Models** | • Lean budgeting & value stream funding • Investment horizon allocation (run/grow/transform) • Business case management • Cost-benefit tracking | Atlassian Align, Planview, Apptio, LeanIX |
| **Capacity Allocation Across Value Streams** | • Value stream capacity mapping • Investment split (features vs. debt vs. platform) • Resource demand forecasting • Capacity vs. demand heat maps | SAFe portfolio Kanban, Planview, custom dashboards |
| **Strategic Dependency Management** | • Cross-product dependency identification • Portfolio-level dependency boards • Dependency risk scoring • Cross-team coordination triggers | Atlassian Align dependency maps, Big Room Planning tools, Miro |
| **Annual / Quarterly Planning Cycles** | • PI Planning facilitation & tooling • Quarterly business review cadence • Planning ceremony templates • Planning outcome documentation | SAFe PI Planning, Miro, Confluence, custom planning tools |

### 1.2 Digital Product Planning

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Product Roadmaps** | • Visual timeline roadmaps • Now/next/later roadmaps • Roadmap versioning & history • Stakeholder-facing roadmap views | Atlassian Jira Plans, Productboard, Aha!, GitHub Projects |
| **Feature Prioritisation** | • RICE / WSJF / MoSCoW scoring • Opportunity scoring models • Impact vs. effort matrices • A/B experiment prioritisation | Jira, Productboard, Airfocus, custom scoring |
| **Outcome Tracking & Product KPIs** | • Product health metrics (adoption, engagement, retention) • Feature usage analytics • Business outcome correlation • Product P&L tracking | Amplitude, Mixpanel, Pendo, custom dashboards |
| **Discovery & Opportunity Mapping** | • User research & interview management • Opportunity solution trees • Assumption mapping & testing • Jobs-to-be-done frameworks | Productboard, Dovetail, Miro, EnjoyHQ |
| **Stakeholder & Customer Feedback Loops** | • Feature request management • NPS / CSAT collection & routing • Support ticket → product insight pipelines • Beta / early access programmes | Canny, Productboard, Intercom, Zendesk insights |
| **Value Stream Mapping** | • End-to-end value flow visualisation • Lead time & cycle time measurement • Waste identification (waiting, handoffs) • Bottleneck analysis & improvement tracking | Miro, Lucidchart, Plutora, custom VSM tools |

### 1.3 Technical Planning

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Sprint / Iteration Planning** | • Sprint goal definition • Story selection & commitment • Sprint capacity calculation • Sprint calendar & ceremony scheduling | Jira, GitHub Projects, Linear, Azure Boards |
| **Backlog Management & Refinement** | • Backlog grooming sessions • Story estimation (points, t-shirt sizing) • Acceptance criteria definition • Backlog health metrics (age, size, staleness) | Jira, Linear, Shortcut, Clubhouse |
| **Capacity & Velocity Tracking** | • Team velocity charts & trends • Sprint burndown / burnup • Cycle time distribution • Predictability metrics | Jira, ActionableAgile, Jellyfish, LinearB |
| **Technical Story & Debt Backlog** | • Dedicated tech debt register • Debt categorisation (code, architecture, infrastructure, test) • Debt cost estimation • Debt reduction progress tracking | Jira with debt labels, SonarQube-linked issues, CodeScene |
| **Dependency & Risk Tracking** | • Cross-team dependency boards • Blocker tracking & escalation • Risk registers with probability/impact • Dependency resolution workflows | Jira dependency links, Align, risk registers |
| **Team-Level Forecasting** | • Monte Carlo simulation for delivery dates • Probabilistic completion forecasts • Scope creep tracking • Schedule confidence intervals | ActionableAgile, Jira forecasting, custom simulations |

### Planning Cascade Flow

```
  ENTERPRISE PLANNING
  ┌──────────────────────────────┐
  │ "Grow payments revenue 30%"  │
  │ "Reduce operational cost"    │
  │ "Achieve SOC2 compliance"    │
  └──────────────┬───────────────┘
                 │  strategic themes & investment allocation
                 ▼
  DIGITAL PRODUCT PLANNING
  ┌──────────────────────────────┐
  │ "Launch merchant self-serve  │
  │  portal by Q3"               │
  │ "Add real-time notifications"│
  └──────────────┬───────────────┘
                 │  features & outcomes decomposed into
                 ▼
  TECHNICAL PLANNING
  ┌──────────────────────────────┐
  │ Sprint 12: Build event       │
  │ consumer, add notification   │
  │ service, update API schema   │
  └──────────────┬───────────────┘
                 │  work items flow into
                 ▼
            SDLC EXECUTION
          (Developer Plane)
```

---

## 3. Layer 2: Engineering & Product Analytics

*The feedback loop — measures everything and serves insights to platform product management, domain product teams, and enterprise leadership.*

### Data Sources — What It Aggregates

```
  Developer Plane ───────────── IDE telemetry, agent usage, template adoption
  Platform Int. & Delivery ──── Service provisioning events, API usage, pipeline runs
  Application & Portfolio ───── Catalog completeness, maturity scores, lifecycle states
  Service Mgmt & Incident ───── Incident volume, MTTR, change frequency
  Observability ─────────────── SLO attainment, alert noise ratios
  Security ──────────────────── Vulnerability density, compliance posture
  OSS Governance ────────────── Dependency health, license compliance rates
  FinOps ────────────────────── Cost per team/service/product, consumption trends
  Infrastructure ────────────── Resource utilisation, capacity metrics
  Knowledge Mgmt ────────────── Documentation coverage, search effectiveness
```

### Shared Analytics Infrastructure

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Data Ingestion & Pipelines** | • Event ingestion from all platform layers (CI/CD events, provisioning events, incident events, cost events) • API polling for systems that don't emit events • Data transformation & normalisation • Real-time and batch processing | Kafka, Airbyte, custom event bus, dbt, Dagster |
| **Analytics Data Platform & APIs** | • Centralised analytics data store (warehouse or lakehouse) • Data model for engineering & product metrics • Query API for programmatic access • Data quality monitoring & freshness SLAs | Snowflake, BigQuery, ClickHouse, custom REST/GraphQL API |
| **Dashboards, Reporting & Self-Service BI** | • Pre-built dashboard templates per analytics domain • Self-service dashboard creation for POs and team leads • Scheduled report generation & distribution • Embeddable widgets for portals & IDEs | Grafana, Looker, Metabase, Superset, Tableau |
| **Alerting on Analytics Thresholds** | • Adoption drop alerts ("Team X stopped using golden paths") • Satisfaction decline alerts • Cost anomaly alerts • Metric regression alerts (DORA scores worsening) | Custom alerting rules, PagerDuty, Slack bots |

### 2.1 Delivery & Engineering Analytics

| Capability | Sub-Capabilities | Who Consumes It | Example Tooling |
|---|---|---|---|
| **DORA Metrics** | • Deployment frequency (per team, product, service) • Lead time for changes • Mean time to recovery (MTTR) • Change failure rate • Filterable by team / product / value stream | Domain product teams, enterprise planning, technical planning | DORA dashboards, Jellyfish, Faros, Haystack, LinearB |
| **Flow Metrics** | • Flow velocity (items completed per time period) • Flow efficiency (active time vs. wait time) • Flow load (WIP per team/value stream) • Flow distribution (features vs. defects vs. debt vs. risk) • Flow time (end-to-end from idea to production) | Digital product planning, enterprise planning | Planview, Tasktop, Jellyfish, custom dashboards |
| **Build & Pipeline Analytics** | • Build success/failure rates per team/service • Build duration trending • Pipeline queue times • Test execution times & flakiness rates • Security scan pass/fail rates | Technical planning, platform product management | GitHub Actions analytics, Datadog CI, custom dashboards |
| **Code & Review Analytics** | • PR cycle time (open to merge) • Review turnaround time • PR size distribution • Code churn rate • Review participation metrics | Technical planning, domain product teams | GitHub Insights, LinearB, Pluralsight Flow |
| **Incident & Reliability Analytics** | • Incident volume by team/product/severity • MTTR by team/product • Incident category analysis (infra, code, config, dependency) • Repeat incident tracking • SLO attainment per team/product | Domain product teams, enterprise planning, service management | PagerDuty Analytics, Rootly, custom dashboards |

### 2.2 Product & Value Analytics

| Capability | Sub-Capabilities | Who Consumes It | Example Tooling |
|---|---|---|---|
| **Feature Adoption & Usage** | • Feature usage rates post-release • Adoption curves (time to target adoption) • Feature engagement depth • Unused feature identification | Digital product planning, domain product teams | Amplitude, Mixpanel, Pendo, PostHog, LaunchDarkly |
| **Product Health Metrics** | • Product-level availability & performance • User-facing error rates • Customer-impacting incident frequency • Product NPS / CSAT correlation with engineering metrics | Digital product planning, enterprise planning | Datadog RUM, Amplitude, custom product health dashboards |
| **Value Stream Mapping Analytics** | • End-to-end lead time from idea to customer value • Bottleneck identification (where does work wait longest?) • Handoff analysis (how many team boundaries does work cross?) • Value delivery cadence | Enterprise planning, digital product planning | Plutora, Planview, custom VSM analytics |
| **Experimentation & A/B Analytics** | • Experiment velocity (experiments run per product per quarter) • Statistical significance tracking • Experiment impact quantification • Winning variant adoption rate | Domain product teams, digital product planning | LaunchDarkly Experimentation, Split, Statsig, Eppo |
| **Business Outcome Correlation** | • Engineering investment → business metric correlation • Deployment frequency → revenue/conversion impact • Reliability → customer retention correlation • Platform adoption → delivery speed impact | Enterprise planning, CFO/CPO | Custom analytics, Jellyfish, Faros |

### 2.3 Developer Productivity & Experience

| Capability | Sub-Capabilities | Who Consumes It | Example Tooling |
|---|---|---|---|
| **SPACE Framework Metrics** | • Satisfaction (survey scores) • Performance (build times, review times, deploy times) • Activity (commits, PRs, deploys — used carefully, never as individual productivity) • Communication (review participation, knowledge sharing) • Efficiency (flow state time, context switches) | Platform product management, technical planning | DX, Pluralsight Flow, Jellyfish, custom surveys |
| **Developer Experience (DevEx) Surveys** | • Periodic satisfaction surveys (quarterly) • Per-capability satisfaction scoring • Friction point identification & trending • NPS for platform services • Qualitative feedback theming & action tracking | Platform product management | DX, custom surveys (Typeform), Qualtrics |
| **Toil & Friction Measurement** | • Time spent on non-value-add activities • Self-service success rate • Manual intervention rate per platform service • Environment provisioning lead time • "Time to first deploy" for new projects | Platform product management, technical planning | Custom toil tracking, pipeline analytics |
| **Onboarding Effectiveness** | • Time-to-first-commit for new joiners • Time-to-first-deploy for new joiners • Onboarding completion rates • New joiner satisfaction scores • Ramp-up time to full productivity | Platform product management, engineering leadership | Custom onboarding dashboards, HR integration |
| **AI & Agent Productivity Impact** | • Copilot / agent suggestion acceptance rates • Agent-generated code quality (defect rate, review feedback) • Time saved through agent-assisted workflows • Agent adoption by team and use case | Platform product management, enterprise planning | Copilot usage dashboards, custom agent analytics |

### 2.4 Platform Analytics (Self-Analytics)

| Capability | Sub-Capabilities | Who Consumes It | Example Tooling |
|---|---|---|---|
| **Platform Service Adoption** | • Adoption rate per platform service (% of eligible teams) • First-use-to-regular-use conversion • Adoption by team, domain, product • Adoption trends over time | Platform SPOs, POs | Custom analytics, Backstage analytics plugin |
| **Platform Health & Reliability** | • Platform service availability (CI/CD, portal, provisioning APIs) • Platform service latency • Platform incident volume & MTTR • Platform SLO attainment | Platform SPOs, POs | Internal SLO dashboards, Prometheus, Datadog |
| **Capability Maturity & Coverage** | • Capability coverage map (exists vs. planned vs. gap) • Maturity level per capability (ad-hoc → optimised) • Coverage by SDLC phase • Capability request pipeline | Platform Head of Product, SPOs | Custom capability heat maps, Backstage |
| **Platform ROI & Unit Economics** | • Engineering hours saved through platform automation • Ticket deflection rate (self-service vs. filed tickets) • Cost per active developer • Cost per deployment • Cost per provisioned environment | Platform Head of Product, enterprise planning | Custom ROI models, FinOps integration |
| **Golden Path & Template Analytics** | • Template usage rate • Template version adoption • Template abandonment analysis • Template satisfaction scoring | Platform POs | Backstage scaffolder analytics |

### 2.5 Quality & Security Analytics

| Capability | Sub-Capabilities | Who Consumes It | Example Tooling |
|---|---|---|---|
| **Code Quality Analytics** | • Code quality score trending per team/product • Test coverage trending • Code smells & duplication metrics • Technical debt ratio | Technical planning, domain product teams | SonarQube, CodeClimate, CodeScene |
| **Security Posture Analytics** | • Vulnerability density per product/team (critical/high/medium/low) • Mean time to remediate vulnerabilities • Compliance posture score trending • Security scorecard attainment | Enterprise planning, security governance, domain product teams | Snyk dashboards, Wiz, custom security dashboards |
| **Dependency Health Analytics** | • Dependency age distribution (how stale are dependencies?) • CVE exposure trending • License compliance rate • OSS health score distribution across portfolio | Security governance, domain product teams, enterprise planning | deps.dev, Snyk, Socket, OpenSSF Scorecard aggregation |
| **Supply Chain Analytics** | • SBOM coverage rate (% of artifacts with SBOMs) • Artifact signing coverage • SLSA level attainment per artifact • Provenance attestation coverage | Security governance, enterprise planning | Sigstore analytics, custom supply chain dashboards |

### 2.6 Executive Dashboards & Reporting

| Capability | Sub-Capabilities | Who Consumes It | Example Tooling |
|---|---|---|---|
| **Enterprise Engineering Dashboard** | • Portfolio-level DORA metrics • Engineering investment split (features/debt/platform/risk) • Cross-product delivery health heat map • Platform adoption summary | CTO, VP Engineering | Custom executive dashboards, Jellyfish |
| **Product Portfolio Dashboard** | • Product health scores (delivery + reliability + cost + adoption) • Product-level cost trending • Value stream performance comparison • Product lifecycle status overview | CPO, VP Product | Custom dashboards, Planview |
| **Risk & Compliance Dashboard** | • Enterprise security posture summary • Critical vulnerability exposure count • Compliance certification status • Open audit findings count | CTO, CISO, CFO | Vanta, Drata, custom risk dashboards |
| **Investment & ROI Dashboard** | • Platform investment vs. measured ROI • Engineering capacity utilisation • Cost efficiency trending • Benchmark comparison (DORA, industry peers) | CTO, CFO, Board | Custom dashboards, Jellyfish, Apptio |
| **Scheduled Report Generation** | • Weekly engineering summary • Monthly product delivery report • Quarterly investment review data pack • Annual platform strategy report | All leadership | Custom reporting, automated slide generation |

---

## 4. Layer 3: Developer Plane

*The persistent experience layer — where developers work across all SDLC phases.*

### 3.1 IDE

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Code Authoring & Editing** | • Syntax highlighting & IntelliSense • Multi-language support • Refactoring tools • Snippet management | VS Code, JetBrains (IntelliJ, WebStorm), Neovim |
| **Integrated Debugging** | • Breakpoint debugging • Variable inspection & watch • Remote debugging • Conditional & log-point debugging | VS Code debugger, JetBrains debugger, Chrome DevTools |
| **Local Development Environments** | • Dev container definitions • Workspace configuration-as-code • Port forwarding & local tunnel • Multi-service local orchestration | GitHub Codespaces, Gitpod, Docker Compose, Tilt, DevPod |
| **IDE Extensions & Marketplace** | • Platform-specific extensions • Security scanner plugins • Linter & formatter integrations • Custom enterprise extension packs | VS Code Marketplace, JetBrains Plugin Repository |
| **Inline AI Assistance** | • Code completion & suggestions • Inline chat & explanation • Code generation from comments • Error explanation & fix suggestions | GitHub Copilot, Codeium, Tabnine, Amazon CodeWhisperer |

### 3.2 Agentic Development Platform

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Coding Agents** | • Multi-file code generation from natural language • Autonomous issue-to-PR workflows • Agent-driven refactoring & migration • Context-aware code suggestions across repos | GitHub Copilot Workspace, Copilot coding agent, Cursor, Devin |
| **Code Review Agents** | • Automated PR review with contextual feedback • Security-focused review (PII, secrets, vulnerabilities) • Architecture & pattern compliance checks • Review summary generation | GitHub Copilot code review, CodeRabbit, Sourcery |
| **Test Generation Agents** | • Unit test generation from function signatures • Integration test scaffolding • Contract test generation from API specs • Test coverage gap identification | Copilot test generation, Diffblue, CodiumAI |
| **Migration Agents** | • Framework version migration (e.g., React 17→18) • Language migration (e.g., Java 11→21) • API migration (deprecated → new endpoints) • Database schema migration generation | Copilot, custom migration agents, OpenRewrite |
| **Triage & Debugging Agents** | • Stack trace analysis & root cause identification • Incident-to-code correlation • Log analysis & anomaly explanation • Suggested fixes from production errors | Copilot, custom triage agents, AI debugging tools |

### 3.3 Fast Prototyping Capabilities

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Rapid Prototyping IDE Tools** | • Low-friction project scaffolding • Instant preview & hot reload • Component-level rapid iteration • Visual prototyping within IDE | Storybook, Vite, HMR tooling, v0.dev |
| **Agent-Assisted Prototyping** | • Natural language → working prototype • Conversational refinement of prototypes • Design spec → functional code generation • Multi-service prototype orchestration | Copilot Workspace, Bolt, Lovable, Replit Agent |
| **Rapid Design-to-Code Flows** | • Figma/design tool → code generation • Wireframe → functional UI • API spec → mock implementation • Data model → CRUD scaffolding | Figma-to-code (Locofy, Anima), OpenAPI generators, Prisma |

### 3.4 SDLC Phase Capabilities — Plan & Design

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Design & API-First Specifications** | • OpenAPI / AsyncAPI spec authoring • Schema-first development workflows • API design review & linting • Contract-first service definition | Swagger Editor, Stoplight Studio, Buf, Spectral |
| **Threat Modeling** | • STRIDE-based threat identification • Data flow diagram creation • Attack surface analysis • Threat model review as part of design process | OWASP Threat Dragon, Microsoft Threat Modeling Tool, IriusRisk |

### 3.5 SDLC Phase Capabilities — Build & Test

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Code & Pair/Agent Coding** | • Human pair programming • AI-assisted coding (Copilot) • Mob programming tooling • Real-time collaboration in editors | GitHub Copilot, VS Code Live Share, Tuple, Pop |
| **Code Review & Quality Gates** | • Pull request review workflows • Automated linting & formatting • Static analysis & code quality scoring • Architecture fitness function checks | GitHub PR reviews, SonarQube, ESLint, Prettier, ArchUnit |
| **Testing & Simulation** | • Unit testing frameworks • Integration & end-to-end testing • Contract testing (consumer/provider) • Performance & load testing • Chaos engineering & fault injection • Security testing (SAST/DAST, integrated) | pytest, Jest, Cypress, Playwright, Pact, k6, Locust, Gremlin, Litmus |

### 3.6 SDLC Phase Capabilities — Deliver & Deploy

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **CI/CD Pipelines** | • Build automation • Test execution orchestration • Security scan integration • Deployment automation | GitHub Actions, Tekton, Jenkins, Dagger |
| **Artifact Management & Registry** | • Container image registry • Package registry (npm, Maven, NuGet) • Artifact versioning & tagging • Artifact signing & provenance | GHCR, Artifactory, ECR, Sigstore/Cosign |
| **Environment Management & Promotion** | • Environment provisioning (dev/staging/prod) • Promotion rules & gates • Environment drift detection • Namespace management | GitOps (ArgoCD, Flux), Terraform, Namespace-as-a-Service |

### 3.7 SDLC Phase Capabilities — Operate & Run

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Release Management & Feature Flags** | • Release scheduling & coordination • Feature flag creation & targeting • Kill switch management • Experimentation & A/B testing | LaunchDarkly, Flipt, Flagsmith, OpenFeature, Split |
| **Canary & Progressive Delivery** | • Canary release automation • Blue/green deployments • Traffic shifting & weighting • Automated rollback on SLO breach | Argo Rollouts, Flagger, Istio traffic management |

---

## 5. Layer 4: Platform Integration & Delivery Services

*The platform's product catalog — self-service capabilities consumed by the Developer Plane.*

### 4.1 API & Service Integration

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **API Gateway & Management** | • Centralised API ingress & routing • Authentication & authorization at the gateway • Request/response transformation • API analytics & usage dashboards | Kong, Apigee, AWS API Gateway, Envoy Gateway |
| **Service Discovery & Registry** | • Dynamic service name resolution • Health-aware routing • Service version management • Service metadata & tagging | Consul, Kubernetes DNS, Eureka, Nacos |
| **API Versioning & Lifecycle** | • Version management (URL, header, content-type) • Deprecation policy enforcement • Consumer migration tracking • Breaking change detection | Optic, Bump.sh, Spectral, custom API lifecycle tooling |
| **Service Mesh Control Plane** | • mTLS between services • Traffic management (retries, timeouts, circuit breaking) • Fault injection for testing • Observability integration (traces, metrics) | Istio, Linkerd, Cilium Service Mesh, Consul Connect |
| **Rate Limiting & Throttling** | • Per-consumer rate limiting • Global & per-route throttling • Quota management & enforcement • Rate limit analytics & alerting | Gateway-level policies, Redis-backed rate limiters, Envoy |
| **External / SaaS Connectors** | • Pre-built integrations to third-party systems • Connector versioning & lifecycle • Authentication management for external APIs • Data mapping & transformation | MuleSoft, Workato, Tray.io, custom connector library |
| **Webhook Management** | • Webhook registration & subscription management • Delivery retry with exponential backoff • Payload signing & verification • Delivery logs & debugging tools | Svix, custom webhook platform, Hookdeck |

### 4.2 Data & Event Services

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Database Provisioning (Self-Service)** | • One-click / CLI database creation • Automated networking & security group configuration • Backup policy configuration • Connection string & credential injection | RDS, Cloud SQL, PlanetScale, CockroachDB + Crossplane/Terraform |
| **Cache Provisioning** | • On-demand managed cache creation • Eviction policy configuration • Cluster sizing recommendations • Cache hit-rate monitoring | ElastiCache, Memorystore, Dragonfly, Redis Cloud |
| **Event Bus / Broker Management** | • Self-service topic creation • Consumer group management • Dead letter queue (DLQ) configuration • Retention & compaction policies | Kafka (Confluent/MSK), SNS/SQS, EventBridge, NATS, Pub/Sub |
| **Schema Registry** | • Central schema storage (Avro, Protobuf, JSON Schema) • Backward/forward compatibility enforcement • Schema evolution tracking • Schema validation in CI/CD | Confluent Schema Registry, Buf, Apicurio, Karapace |
| **Data Catalog & Lineage** | • Dataset discovery & search • Data ownership & stewardship assignment • Column-level lineage tracking • Data quality scoring | DataHub, OpenMetadata, Amundsen, Atlan |
| **Streaming & ETL Pipelines** | • Templated batch & real-time pipelines • Connector management (source/sink) • Pipeline monitoring & alerting • Transformation authoring (SQL, Python) | Flink, Spark, Airbyte, dbt, Fivetran, Dagster |
| **Object / Blob Storage Services** | • Managed bucket/container creation • Lifecycle policies (tiering, expiry) • Access policy management • CDN integration for static assets | S3, GCS, Azure Blob, MinIO |
| **Data Access Governance** | • Column/row-level access policies • PII masking & tokenisation • Audit logging on data access • Data classification & tagging | Apache Ranger, Immuta, Privacera, platform policy-as-code |

### 4.3 Delivery & Runtime Orchestration

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **CI/CD Engine & Pipeline Templates** | • Shared workflow / pipeline libraries • Reusable build, test, scan, deploy steps • Pipeline-as-code authoring • Pipeline execution analytics | GitHub Actions (reusable workflows), Tekton, Dagger, Jenkins shared libraries |
| **GitOps Controllers** | • Declarative Git-driven deployment reconciliation • Drift detection & auto-remediation • Multi-cluster deployment orchestration • Promotion between environments via Git | ArgoCD, Flux, Rancher Fleet |
| **Artifact Registry & Signing** | • Immutable, versioned artifact storage • Cosign / Sigstore artifact signing • Provenance attestation (SLSA) • Vulnerability scanning of stored artifacts | GHCR, Artifactory, ECR, Harbor + Cosign/Sigstore |
| **Environment-as-Code** | • Declarative environment definitions • On-demand ephemeral environments • Environment cloning & seeding • Environment configuration drift detection | Terraform, Pulumi, Crossplane, Namespace-as-a-Service |
| **Deployment Targets & Promotion Rules** | • Target environment definitions (dev/staging/canary/prod) • Promotion gate configuration (manual, automated, SLO-based) • Deployment window & freeze management • Multi-region deployment orchestration | ArgoCD ApplicationSets, custom promotion controllers |
| **Feature Flag Infrastructure** | • Flag evaluation engine (server-side & client-side) • Targeting rules (user segments, percentages, attributes) • Flag lifecycle management (archive, cleanup) • Flag audit logging | LaunchDarkly, Flipt, Flagsmith, OpenFeature SDK |
| **Progressive Delivery Engine** | • Canary analysis automation • Blue/green traffic switching • A/B traffic routing • Automated rollback on metric degradation | Argo Rollouts, Flagger, Istio traffic management |
| **Rollback & Recovery Policies** | • Automated rollback triggers (health check, SLO breach) • Deployment circuit breakers • Safe recovery procedures & runbooks • Post-rollback notification & incident creation | Health-check-based rollback, ArgoCD auto-sync, custom controllers |

### 4.4 Developer Self-Service Interfaces

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Internal Developer Portal** | • Unified web UI for all platform services • Personalised developer home page • Activity feeds & notifications • Search across all platform resources | Backstage, Port, Cortex, OpsLevel |
| **Service Catalog (Requestable)** | • Browsable inventory of platform offerings • One-click provisioning of resources • Request tracking & approval workflows • Usage analytics per offering | Backstage catalog, Port self-service, custom portal |
| **Golden Path Templates** | • Opinionated project starters (app, service, library) • Pre-wired CI/CD, observability, security • Template versioning & lifecycle • Template usage analytics & compliance tracking | Backstage software templates, Cookiecutter, Yeoman, custom CLI |
| **CLI & API for Platform Actions** | • Command-line access to all platform services • RESTful / gRPC platform control plane API • Scriptable automation for platform tasks • CLI auto-update & plugin system | Custom platform CLI, Terraform provider, REST/gRPC API |
| **Documentation & Onboarding Guides** | • Living platform documentation • Getting-started tutorials per capability • Interactive walkthroughs & sandboxes • API reference documentation (auto-generated) | Backstage TechDocs, Docusaurus, Notion, ReadMe |

### 4.5 Configuration & Secrets Management

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Secrets Injection & Rotation** | • Dynamic secrets delivery to workloads • Automated rotation on schedule or trigger • Zero-downtime rotation workflows • Secrets access audit logging | HashiCorp Vault, AWS Secrets Manager, External Secrets Operator |
| **Config-as-Code** | • Version-controlled application configuration • Environment-specific overrides • Configuration validation in CI • Configuration change audit trail | Kustomize, Helm values, Spring Cloud Config, ConfigMaps |
| **Feature Flag Configuration** | • Targeting rule management • Default values & rollout percentages • Flag dependency tracking • Configuration change history | LaunchDarkly admin, Flipt admin, OpenFeature management API |
| **Environment Variable Management** | • Centralised env var management per service/environment • Env var validation & schema enforcement • Secret vs. non-secret classification • Env var propagation to runtime | Platform portal, sealed secrets, doppler, dotenv-vault |
| **Certificate Management** | • Automated TLS certificate issuance • Auto-renewal before expiry • Certificate distribution to load balancers & workloads • Certificate transparency logging & monitoring | cert-manager, Let's Encrypt, AWS ACM, Venafi |

### 4.6 Platform Extensibility

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Platform API & SDK** | • RESTful / gRPC control plane API • Client libraries in multiple languages • API authentication & RBAC • API versioning & backward compatibility | Custom platform API, gRPC services, SDK libraries |
| **Custom Resource Definitions** | • Domain-specific resource abstractions • Composition & packaging of multi-resource bundles • Validation webhooks & defaulting • Reconciliation controllers | Kubernetes CRDs, Crossplane Compositions & XRDs |
| **Plugin / Extension Framework** | • Portal plugin architecture (frontend & backend) • Pipeline custom action/task framework • CLI plugin system • Extension marketplace / registry | Backstage plugins, GitHub Actions custom actions, Tekton custom tasks |
| **Terraform / Crossplane Providers** | • Platform-native Terraform providers • Crossplane provider packages • Provider versioning & release • Documentation & examples | Custom Terraform providers, Crossplane provider packages |
| **Backstage Plugins** | • Custom frontend widgets & pages • Backend plugin APIs • Integration with internal systems • Plugin quality & security review | Backstage frontend/backend plugins, community plugins |

### 4.7 Sandbox & Rapid Provisioning

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **On-Demand Ephemeral Environments** | • Instant environment creation from PR or branch • Pre-wired with platform services (DB, queue, cache) • Automatic teardown after TTL or PR close • Shareable preview URLs | Gitpod, Codespaces, Namespace-as-a-Service, Uffizzi |
| **Prototype-Grade Infrastructure** | • Lightweight, cost-optimised dev-tier resources • Mock services for external dependencies • Local-to-cloud bridge for hybrid development • Pre-seeded test data | Dev-tier RDS, LocalStack, WireMock, Testcontainers |
| **Experiment Tracking & Teardown** | • Active prototype inventory • Auto-expire policies (TTL-based cleanup) • Cost tracking per experiment • Sandbox sprawl alerting | Custom TTL controllers, Janitor tools, FinOps tagging |

---

## 6. Layer 5: Application & Portfolio Management

*The portfolio governance layer — what we've built, who owns it, and is it still fit for purpose.*

### 5.1 Software System Catalog

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **System Registry** | • Authoritative inventory of all systems (apps, services, batch jobs, libraries) • System type classification (frontend, backend, data pipeline, etc.) • System status (active, deprecated, sunset, archived) • Repository & artifact linkage | Backstage catalog, OpsLevel, Port, ServiceNow CMDB |
| **Ownership & Team Mapping** | • System → team ownership assignment • Escalation contact per system • Domain & sub-domain alignment • Ownership transfer workflows | Backstage ownership, OpsLevel teams, PagerDuty service directory |
| **System Dependency Graphs** | • Runtime dependency visualisation (API calls, event subscriptions) • Build-time dependency tracking (shared libraries, packages) • Database & queue dependency mapping • Dependency graph auto-discovery vs. manual declaration | Backstage dependency graph, Datadog service map, custom Neo4j |
| **Architecture Decision Records (ADRs)** | • Structured decision capture (context, decision, consequences) • ADR lifecycle (proposed, accepted, superseded, deprecated) • ADR linkage to systems & components • Searchable ADR repository | ADR files in repo (Markdown), Backstage ADR plugin, Log4brains |
| **Tech Stack & Language Registry** | • Automated language & framework detection per repo • Framework version tracking • Runtime version tracking (Node, Java, Python, .NET) • End-of-life / end-of-support alerting | Backstage tech insights, GitHub Linguist, custom repo scanning |
| **API Surface Area Per System** | • List of all APIs exposed by a system (REST, gRPC, GraphQL, event) • APIs consumed by a system • API specification linkage (OpenAPI, AsyncAPI) • API health & usage metrics per system | OpenAPI/AsyncAPI aggregation, API catalog, Backstage API entity |

### 5.2 Digital Product Catalog

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Product Registry** | • Inventory of digital products with business descriptions • Product owner & stakeholder mapping • Product status (incubation, growth, mature, sunset) • Product documentation & vision statements | Custom product catalog, Backstage with domain model, Port |
| **Product ↔ System ↔ Service Mapping** | • Hierarchical mapping: product → system → component → service • Visual product composition views • Gap analysis (products without mapped systems) • Cross-product shared service identification | Backstage domain/system/component hierarchy, Port blueprints, LeanIX |
| **Business Capability Mapping** | • Enterprise capability model definition • Capability → product → system alignment • Capability heat maps (investment, health, risk) • Strategic gap identification | LeanIX, Ardoq, custom capability model, TOGAF-aligned tools |
| **Customer Journey ↔ System Tracing** | • Critical journey identification (e.g., checkout, onboarding) • Journey step → system mapping • Journey health monitoring (latency, error rate per step) • Journey-aware incident prioritisation | Custom journey maps, Datadog Synthetics mapped to catalog |
| **Product KPIs & Value Stream Metrics** | • DORA metrics per product (deployment frequency, lead time, MTTR, change failure rate) • Business metrics correlation (revenue, conversion, engagement) • Value stream flow metrics (flow velocity, flow efficiency) • Product health dashboards | DORA dashboards, Jellyfish, Faros, Haystack, custom dashboards |
| **Cost Attribution Per Product** | • Infrastructure cost allocated to products • Team cost allocation • Cost trend analysis & forecasting • Cost efficiency scoring (cost per transaction, cost per user) | Kubecost, Vantage, CloudHealth, Apptio, custom FinOps dashboards |

### 5.3 Application Lifecycle Management

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **App Health & Maturity Scoring** | • Composite health score (code quality + test coverage + security + observability + docs) • Automated score calculation from tool integrations • Score trending & historical comparison • Team-level and portfolio-level dashboards | Backstage Scorecards, OpsLevel Checks, Port Scorecards, Cortex |
| **Tech Debt Tracking** | • Debt item registration & categorisation (code, architecture, infra, test, dependency) • Debt cost estimation (effort to remediate, risk of inaction) • Debt prioritisation frameworks • Debt reduction sprint allocation & progress tracking | SonarQube (technical debt ratio), CodeScene, custom debt registers |
| **Deprecation & Sunset Planning** | • System lifecycle state management (active → deprecated → sunset → archived) • Consumer notification & migration timelines • Traffic monitoring during wind-down • Automated decommissioning checklists | Custom lifecycle states in catalog, migration trackers |
| **Migration & Modernisation Tracking** | • Migration programme definition (e.g., monolith → microservices, on-prem → cloud) • System-level migration status tracking • Migration dependency identification • Progress dashboards & reporting | Backstage migration dashboard, custom Jira projects, LeanIX |
| **Version & Release History** | • Historical release log per system • Changelog aggregation • Release → incident correlation • Release cadence tracking | GitHub Releases, semantic-release, catalog-linked release data |
| **Compliance & Regulatory Status** | • Regulatory scope tagging per system (SOC2, PCI, GDPR, HIPAA) • Compliance evidence linkage • Compliance gap tracking • Re-certification scheduling | Vanta, Drata, custom compliance metadata in catalog |
| **Fitness Function Monitoring** | • Automated architecture fitness tests in CI • Continuous fitness score evaluation • Threshold alerting on fitness degradation • Fitness function library & templates | ArchUnit, custom fitness functions, catalog-driven threshold checks |

### 5.4 Dependency & Topology Management

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **System-to-System Dependency Maps** | • Directed graph of runtime & build-time dependencies • Auto-discovered (from traces, API calls, imports) + manually declared • Dependency strength scoring (critical vs. optional) • Circular dependency detection | Backstage, Datadog service map, custom Neo4j graph |
| **Upstream / Downstream Impact Analysis** | • "What breaks if I change this?" queries • Consumer identification for shared services/APIs • Impact radius scoring • Change impact reports generated pre-deployment | Graph queries, automated impact reports, custom tooling |
| **Blast Radius Visualisation** | • Failure propagation path visualisation • Cascading failure simulation • Zone/region-aware blast radius • Historical incident blast radius overlay | PagerDuty service graph, Gremlin, custom dashboards |
| **Infrastructure Dependency Mapping** | • System → infrastructure resource mapping (DB, queue, cache, storage) • Cloud resource dependency graph • Shared infrastructure identification • Infrastructure change impact analysis | Crossplane resource tree, cloud asset inventory, Backstage resource links |

### 5.5 Standards & Governance

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Golden Path Compliance Scoring** | • Measure adherence to recommended patterns (CI/CD, observability, security, testing) • Per-system compliance dashboard • Non-compliance alerting & remediation guidance • Compliance trending over time | Backstage Scorecards, OpsLevel service maturity, Port Scorecards |
| **Architecture Guardrails** | • Automated rules preventing architectural drift • Domain boundary enforcement (no cross-boundary DB access) • Communication pattern enforcement (sync vs. async) • Guardrail violation reporting & exemption workflows | ArchUnit, Spectral, OPA/Rego policies, CI-based checks |
| **Technology Radar & Approved Tech List** | • Adopt / Trial / Assess / Hold categorisation • Language, framework, and library recommendations • Radar update cadence & governance process • Enforcement via pipeline gates or advisory alerts | Thoughtworks-style radar, Backstage tech radar plugin, custom lists |
| **Scorecard & Maturity Models** | • Multi-dimensional maturity assessment (security, reliability, observability, documentation, testing) • Level-based maturity progression (L1–L5) • Maturity improvement plans • Portfolio-level maturity heat maps | Backstage Scorecards, OpsLevel Checks, custom maturity models |
| **Policy Enforcement & Exemption Management** | • Policy-as-code definition & automated enforcement • Exemption request & approval workflows • Exemption expiry dates & renewal tracking • Policy coverage & enforcement analytics | OPA/Kyverno with exemption registry, custom governance portal |

### 5.6 Technology Audit Service

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **On-Demand Technology Assessments** | • Structured audit templates (architecture, security, operability, code quality) • Team-requested or governance-triggered assessments • Assessment scoring & benchmarking • Prioritised recommendation reports | Custom audit framework, assessment templates, Confluence |
| **Architecture Fitness Reviews** | • Design-goal alignment evaluation • Non-functional requirement (NFR) validation • Scalability & performance assessment • Architecture evolution recommendations | ArchUnit, custom fitness tests, architect-led reviews |
| **Tech Debt Quantification** | • Costed debt register with effort estimates • Risk-weighted prioritisation • Debt-to-feature investment ratio analysis • Remediation ROI modelling | CodeScene, SonarQube, custom debt scoring models |
| **Migration Readiness Assessments** | • Cloud readiness evaluation • Containerisation readiness scoring • Microservices decomposition feasibility • Data migration complexity analysis | Custom assessment checklists, AWS Migration Hub, Azure Migrate |
| **Vendor & Technology Risk Reviews** | • End-of-life / end-of-support risk assessment • Vendor lock-in evaluation • Community health scoring (for OSS) • Alternative technology identification | Technology radar, custom risk matrices, deps.dev |
| **Compliance & Regulatory Audits** | • Regulatory requirement mapping to systems • Evidence gathering automation • Gap analysis & remediation planning • Audit report generation & finding tracking | Vanta, Drata, custom audit workflows, Jira-linked findings |
| **Audit Report Generation & Tracking** | • Structured finding reports with severity ratings • Recommendation tracking with owners & due dates • Re-audit scheduling • Portfolio-level audit status dashboard | Custom reporting, Confluence, Jira-linked findings |

---

## 7. Layer 6: Service Management & Incident Management

*The operational lifecycle layer — how we run, change, and recover production services.*

### 6.1 Service Catalog & Ownership

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Operational Service Catalog** | • Runtime service inventory (focused on deployed instances) • Service tier classification (Tier 0/1/2/3) • SLA/SLO assignment per service • Service dependency for incident impact assessment | PagerDuty service directory, ServiceNow CMDB, Backstage |
| **Ownership & Accountability** | • Service → team → on-call mapping • Escalation path definition • Ownership validation & orphan service detection • Accountability matrix (RACI) per service | PagerDuty, OpsLevel, Backstage ownership |

### 6.2 Change Management & Approval Flows

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Change Request Management** | • Change request creation & classification (standard, normal, emergency) • Risk assessment & scoring • Change calendar & scheduling • Change conflict detection | ServiceNow Change Management, custom GitOps-based change management |
| **Approval Workflows** | • Role-based approval routing • Automated approval for low-risk changes • Emergency change fast-track process • Approval audit trail | GitHub PR approvals, ServiceNow, custom approval bots |
| **Deployment Freeze Management** | • Freeze window definition & enforcement • Freeze exception process • Pre/post-freeze readiness checks • Freeze calendar integration with CI/CD | Custom freeze controllers, PagerDuty maintenance windows |
| **Change Audit & Compliance** | • Full change history with traceability (commit → PR → build → deploy) • Compliance evidence for SOC2/PCI audits • Change failure rate tracking • Post-change verification | GitOps audit trail, ServiceNow, DORA change failure rate metrics |

### 6.3 Incident Detection, Triage & Resolution

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Incident Detection** | • Alert-driven incident creation • Anomaly-based incident detection (AIOps) • Customer-reported incident ingestion • Synthetic monitoring-triggered incidents | PagerDuty, Opsgenie, Datadog + PagerDuty integration |
| **Incident Triage** | • Severity classification (SEV1–4) • Automated triage suggestions (AI-assisted) • Impact assessment using dependency graphs • Incident commander assignment | Rootly, FireHydrant, PagerDuty, custom triage bots |
| **Incident Response** | • War room / incident channel creation • Stakeholder communication (status pages, comms templates) • Timeline tracking & documentation • Customer communication management | Rootly, FireHydrant, Statuspage, incident.io |
| **Post-Incident Review** | • Blameless postmortem facilitation • Root cause analysis (5 Whys, fishbone) • Action item tracking & follow-through • Postmortem knowledge base & pattern analysis | Rootly, FireHydrant, Confluence, custom postmortem templates |

### 6.4 On-Call, Escalation & Runbook Automation

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **On-Call Management** | • Rotation scheduling • Override & swap management • On-call load balancing & fairness tracking • On-call compensation tracking | PagerDuty, Opsgenie, Grafana OnCall |
| **Escalation Policies** | • Multi-level escalation chains • Time-based auto-escalation • Severity-aware escalation routing • Cross-team escalation for shared services | PagerDuty, Opsgenie, custom escalation rules |
| **Runbook Automation** | • Documented runbooks linked to alerts • Semi-automated runbook execution • Fully automated remediation for known issues • Runbook effectiveness tracking | Rundeck, Shoreline.io, PagerDuty Automation Actions, custom bots |
| **Incident Communication** | • Automated status page updates • Internal stakeholder notifications • Customer-facing communication templates • Communication timeline management | Statuspage, incident.io, FireHydrant, custom Slack bots |

---

## 8. Layer 7: Observability & Monitoring

*The sensory system — captures signals from infrastructure and applications, feeds upward into operations and back to developers.*

### 7.1 Metrics

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Infrastructure Metrics** | • CPU, memory, disk, network utilisation • Container & pod resource metrics • Cloud service metrics (RDS, Lambda, etc.) • Cluster health metrics | Prometheus, Datadog, CloudWatch, Grafana |
| **Application Metrics** | • Request rate, error rate, duration (RED) • Custom business metrics • Saturation metrics (queue depth, connection pool) • Dependency health metrics | Prometheus client libraries, Datadog APM, StatsD, OpenTelemetry |
| **Metric Aggregation & Storage** | • Long-term metric storage • Down-sampling & retention policies • Cross-environment metric federation • Metric cardinality management | Thanos, Cortex, Mimir, Datadog, Victoria Metrics |

### 7.2 Logging

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Log Collection & Aggregation** | • Structured log collection from all sources • Log shipping & buffering • Multi-environment log aggregation • Log format standardisation | Fluentd, Fluent Bit, Logstash, Vector, Datadog Agent |
| **Log Storage & Search** | • Centralised log storage • Full-text search & filtering • Log retention policies • Log archive & compliance retention | Elasticsearch (ELK), Loki, Splunk, Datadog Logs |
| **Log Analysis** | • Pattern detection & anomaly identification • Log-based alerting • Correlation across services • AI-powered log summarisation | Splunk ITSI, Datadog Log Analytics, Elastic ML |

### 7.3 Tracing

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Distributed Tracing** | • End-to-end request tracing across services • Trace context propagation (W3C Trace Context) • Span-level performance analysis • Trace-based error identification | OpenTelemetry, Jaeger, Tempo, Datadog APM, Zipkin |
| **Trace Sampling & Storage** | • Head-based & tail-based sampling • Sampling policy configuration • Trace retention & archival • Trace storage cost management | OpenTelemetry Collector, Jaeger, Tempo, Datadog |
| **Trace Analysis & Visualisation** | • Service dependency map from traces • Critical path analysis • Latency breakdown per span • Trace comparison (before/after deployment) | Jaeger UI, Grafana Tempo, Datadog APM, Honeycomb |

### 7.4 Alerting & AIOps

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Alert Definition & Management** | • Threshold-based alerting • Anomaly-based alerting • Alert routing & notification channels • Alert suppression & maintenance windows | Alertmanager, Datadog Monitors, PagerDuty, Grafana Alerting |
| **Alert Correlation & Noise Reduction** | • Alert grouping & deduplication • Root cause correlation across alerts • Alert storm suppression • Service-aware alert routing | BigPanda, PagerDuty AIOps, Moogsoft, Datadog Watchdog |
| **AIOps & Intelligent Operations** | • Anomaly detection on metrics & logs • Predictive alerting (forecast-based) • Automated root cause suggestions • Change-correlated anomaly detection | Datadog Watchdog, Dynatrace Davis, BigPanda, Moogsoft |

### 7.5 SLO/SLI Management

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **SLI Definition** | • Indicator selection (availability, latency, error rate, throughput) • SLI source configuration (metrics, logs, synthetic checks) • SLI validation & accuracy testing • SLI documentation per service | OpenSLO spec, Datadog SLOs, Nobl9 |
| **SLO Tracking** | • Error budget calculation & tracking • Burn-rate alerting • SLO dashboard per team/service • SLO historical trending | Nobl9, Datadog SLOs, Sloth, Google SLO Generator |
| **Error Budget Policy** | • Error budget consumption alerting • Automated deployment freeze on budget exhaustion • Error budget allocation (feature vs. reliability work) • Error budget review cadence | Custom policies, Nobl9, team-level governance |

---

## 9. Layer 8 (Cross-Cutting): Knowledge Management

*Organisational memory — every layer produces and consumes knowledge.*

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Design & Technical Documentation** | • Architecture documentation (C4 model, diagrams) • API documentation (auto-generated & hand-written) • Design proposals & RFCs • Technical specification templates | Confluence, Backstage TechDocs, Notion, GitHub Wiki, Structurizr |
| **Operational Knowledge** | • Runbooks & standard operating procedures • Incident postmortem repository • Disaster recovery documentation • Troubleshooting guides & decision trees | Confluence, Rootly postmortems, PagerDuty runbooks, Notion |
| **Learning & Onboarding** | • Platform onboarding guides & tutorials • New joiner engineering bootcamp content • Coding standards & style guides • Video walkthroughs & recorded demos | Confluence, LMS (Udemy Business, Pluralsight), Backstage docs |
| **Decision Records & Governance Documentation** | • Architecture Decision Records (ADRs) • Technology radar rationale & meeting notes • Policy documents & exemption records • Governance process documentation | ADR files in repos, Log4brains, Confluence, Backstage ADR plugin |
| **Product & Strategy Knowledge** | • Product vision & strategy documents • OKR context & rationale • Customer research findings & insights • Retrospective outcomes & improvement actions | Confluence, Notion, Productboard insights, Miro boards |
| **Search & Discovery** | • Unified search across all knowledge sources • AI-powered Q&A over documentation • Auto-tagging & categorisation • Stale content detection & archival | Confluence search, Glean, Guru, custom RAG pipelines, Stack Overflow for Teams |

---

## 10. Layer 9 (Cross-Cutting): Open Source Governance & Enablers

*Governs how the organisation consumes, contributes to, and manages open source software.*

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **License Compliance & Policy** | • Approved license list definition (MIT, Apache 2.0, BSD, etc.) • License detection in dependencies • Non-compliant license blocking in CI/CD • License obligation tracking & fulfilment | FOSSA, Snyk, Black Duck, GitHub license detection, Licensee |
| **OSS Consumption Governance** | • Approved / vetted OSS library list • Version pinning & update policies • Vulnerability monitoring for consumed packages • Dependency age & health scoring | Dependabot, Renovate, Snyk, Socket, deps.dev |
| **InnerSource Enablement** | • InnerSource repository guidelines (CONTRIBUTING, CODEOWNERS) • Cross-team contribution workflows • Internal package registry for shared libraries • InnerSource metrics (contributions, adoption) | GitHub InnerSource patterns, internal registries, contribution guidelines |
| **Contribution & Community Management** | • External OSS contribution policy (IP review, approval process) • CLA / DCO management • Corporate branding & attribution guidelines • Community engagement tracking | CLA bots (CLA Assistant), DCO bot, OSPO tooling |
| **OSS Health & Risk Monitoring** | • Consumed package health scoring (maintainer activity, release cadence) • Bus factor analysis for critical dependencies • CVE velocity tracking per package • Unmaintained dependency alerting | OpenSSF Scorecard, deps.dev, Socket, Snyk Advisor |
| **SBOM Management** | • SBOM generation for all build artifacts (CycloneDX, SPDX) • Central SBOM registry & storage • SBOM-based vulnerability correlation • SBOM sharing with customers & partners (on request) | Syft, Trivy, Grype, SPDX tools, CycloneDX tools, GUAC |

---

## 11. Layer 10 (Cross-Cutting): FinOps

*Financial governance across the entire platform — cost visibility, consumption accountability, and optimisation.*

### 10.1 Cost Visibility & Allocation

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Cloud Cost Aggregation** | • Multi-cloud cost ingestion (AWS, Azure, GCP) • Cost normalisation across providers • Discount & commitment tracking (RIs, savings plans, CUDs) • Amortised vs. on-demand cost views | Vantage, CloudHealth, AWS Cost Explorer, GCP Billing, Azure Cost Mgmt |
| **Platform Service Cost Tracking** | • Cost of running platform services (CI/CD infra, portal, registries, Vault) • Cost per platform capability • Platform team headcount cost allocation • Tooling & license cost tracking | Custom dashboards, Apptio, vendor billing APIs |
| **Cost Allocation & Tagging** | • Mandatory tag enforcement (team, service, environment, product) • Tag compliance scoring & remediation • Untagged resource identification & alerting • Tag hierarchy (product → system → service → environment) | Cloud tagging policies, Kubecost, custom tag enforcement |
| **Multi-Dimensional Cost Views** | • Cost by team / squad / tribe • Cost by product / value stream • Cost by environment (dev/staging/prod) • Cost by service / component • Cost by SDLC phase (build vs. run) | Kubecost, Vantage, custom Looker/Grafana dashboards |

### 10.2 Consumption Metering & Rating

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Resource Consumption Metering** | • Compute hours per team/service • Storage GB per team/service • Network egress per team/service • Database instance-hours per team/service | Kubecost, cloud billing APIs, custom metering agents |
| **Platform Service Consumption Metering** | • CI/CD pipeline minutes consumed • Artifact registry storage consumed • Environments provisioned (count, duration, size) • API gateway request volume per consumer • Secrets managed per team • Observability data volume (logs, metrics, traces) per team | Custom metering platform, vendor usage APIs |
| **Unit Cost Rating** | • Cost per pipeline minute • Cost per GB of log storage • Cost per environment-hour • Cost per API request • Cost per secret rotation • Rate card publication for all platform services | Custom rate card engine, FinOps tooling |
| **Consumption Forecasting** | • Trend-based cost projection per team/product • Seasonality-aware forecasting • Capacity-driven cost modelling • What-if cost simulation for new services | Vantage, custom forecasting, cloud billing forecasts |

### 10.3 Cross-Charging & Showback

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Showback Reporting** | • Monthly consumption reports per team/product • Itemised bills showing platform service usage • Cost comparison (month-over-month, quarter-over-quarter) • Anomaly highlights ("your CI/CD cost increased 40%") | Custom showback portal, Kubecost, Vantage, Apptio |
| **Chargeback Execution** | • Automated cost allocation to cost centres • Internal invoice generation • Finance system integration (SAP, Oracle, Workday) • Chargeback dispute & correction workflows | Apptio, CloudHealth, custom finance integration |
| **Consumption Budgets & Alerts** | • Team/product-level budget setting • Budget burn-rate alerting (50%, 75%, 90% thresholds) • Forecasted overspend early warning • Budget approval workflows for burst capacity | AWS Budgets, GCP Budget alerts, custom budget management |
| **Self-Service Cost Visibility** | • Cost dashboard in internal developer portal • Real-time cost view per service in IDE/CLI • Cost impact preview before provisioning ("this DB will cost ~$X/month") • Cost leaderboards (gamification of efficiency) | Backstage FinOps plugin, Infracost (PR cost preview), custom portal widgets |

### 10.4 Financial Governance & Optimisation

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Right-Sizing Recommendations** | • Compute right-sizing (over-provisioned pods/VMs) • Database right-sizing (instance class, storage) • Cache right-sizing • Automated right-sizing action (with approval) | Kubecost, AWS Compute Optimizer, GCP Recommender, Spot.io |
| **Waste Detection & Elimination** | • Idle resource identification (unused DBs, orphaned volumes, stale environments) • Non-production environment cost governance (auto-shutdown, TTL) • Unused license detection • Sandbox sprawl cost tracking | Kubecost, Vantage, custom janitor jobs, FinOps dashboards |
| **Commitment & Discount Management** | • Reserved Instance / Savings Plan coverage analysis • Commitment purchase recommendations • Spot / preemptible instance utilisation • Commitment utilisation tracking & optimisation | AWS Cost Explorer, GCP CUD analysis, Spot.io, CloudHealth |
| **Cost-Aware Architecture Guidance** | • Cost-aware golden path templates (default to cost-efficient configurations) • Architecture review cost impact assessment • Cost benchmarking across similar services • Cost efficiency scoring in maturity scorecards | Infracost, custom cost guidelines, architecture review checklists |
| **FinOps Governance & Accountability** | • FinOps policy definition & enforcement (e.g., "no untagged resources", "dev environments must auto-shutdown") • Cost review cadence per team (monthly cost reviews) • FinOps champion network (embedded cost advocates per team) • Escalation for teams exceeding budgets • FinOps maturity assessment (crawl/walk/run per team) | Custom governance portal, FinOps Foundation framework, team scorecards |

---

## 12. Layer 11 (Cross-Cutting): Security Services

*Protects every layer — from code to runtime — as a cross-cutting concern embedded throughout the SDLC.*

### 11.1 Identity & Access Management

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **User Identity** | • Single sign-on (SSO) • Multi-factor authentication (MFA) • Directory integration (LDAP, Azure AD, Okta) • Session management & token lifecycle | Okta, Azure AD, Auth0, Keycloak |
| **Workload Identity** | • Service-to-service identity (SPIFFE/SPIRE) • Cloud IAM roles for workloads • Short-lived credential issuance • Identity federation across clusters/clouds | SPIFFE/SPIRE, AWS IAM Roles for Service Accounts, GKE Workload Identity |
| **Authorization** | • Role-based access control (RBAC) • Attribute-based access control (ABAC) • Policy-as-code authorization (OPA/Cedar) • Fine-grained permission management | OPA, Cedar, Casbin, Kubernetes RBAC, cloud IAM policies |
| **Privileged Access Management** | • Just-in-time (JIT) access provisioning • Break-glass procedures • Privileged session recording • Access request & approval workflows | CyberArk, HashiCorp Boundary, Teleport, StrongDM |

### 11.2 AppSec & Code Security

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Static Application Security Testing (SAST)** | • Source code vulnerability scanning • Custom rule authoring • IDE-integrated scanning (shift-left) • False positive management & suppression | Semgrep, CodeQL, SonarQube, Checkmarx |
| **Dynamic Application Security Testing (DAST)** | • Running application vulnerability scanning • API security testing • Authenticated scanning workflows • DAST in CI/CD pipelines | OWASP ZAP, Burp Suite, Invicti, StackHawk |
| **Infrastructure-as-Code Scanning** | • Terraform / CloudFormation / Helm misconfigurations • Kubernetes manifest security checks • Docker image hardening validation • Policy-as-code for IaC | Checkov, tfsec, Trivy, Kics, Snyk IaC |
| **Secrets Detection** | • Pre-commit secrets scanning • CI/CD secrets scanning • Historical secrets scanning (git history) • Secrets revocation workflow integration | GitLeaks, TruffleHog, GitHub secret scanning, detect-secrets |

### 11.3 Supply Chain Security

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Dependency Scanning** | • Known vulnerability detection (CVE matching) • Transitive dependency analysis • Reachability analysis (is the vulnerable code actually called?) • Automated remediation PRs | Dependabot, Snyk, Grype, Trivy, Socket |
| **Artifact Signing & Verification** | • Container image signing (Cosign) • Build provenance attestation (SLSA) • Signature verification at deployment • Signed SBOM distribution | Sigstore (Cosign, Fulcio, Rekor), Notary v2, in-toto |
| **Build Pipeline Security** | • Hermetic builds (isolated build environments) • Build reproducibility verification • Pipeline tampering detection • SLSA level compliance tracking | SLSA framework, Tekton Chains, GitHub artifact attestation |
| **Container Image Security** | • Base image vulnerability scanning • Base image provenance & trust • Image hardening policies (no root, minimal base) • Registry admission policies | Trivy, Snyk Container, Docker Scout, Kyverno admission policies |

### 11.4 Runtime Security & Compliance

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Runtime Threat Detection** | • Container runtime anomaly detection • File integrity monitoring • Process execution monitoring • Network anomaly detection | Falco, Sysdig Secure, Aqua, Prisma Cloud |
| **Web Application Firewall (WAF)** | • OWASP Top 10 protection • Bot detection & mitigation • Rate limiting & DDoS protection • Custom WAF rules | AWS WAF, Cloudflare WAF, Fastly, Akamai |
| **Network Security** | • Network policy enforcement (microsegmentation) • Egress filtering & control • Service mesh mTLS enforcement • DNS-based threat detection | Cilium, Calico, Istio network policies, cloud security groups |
| **Continuous Compliance Monitoring** | • Policy-as-code enforcement at runtime • Configuration drift detection • Compliance posture dashboards • Automated remediation for compliance violations | OPA/Gatekeeper, Kyverno, Prisma Cloud, Wiz, Bridgecrew |
| **Data Protection** | • Encryption at rest & in transit enforcement • PII detection & masking in runtime data • Data loss prevention (DLP) policies • Key rotation & management | AWS KMS, GCP KMS, HashiCorp Vault Transit, Nightfall |

---

## 13. Layer 12 (Cross-Cutting): Infrastructure & Resource Services

*The foundational layer — raw compute, data, networking, and resource management consumed by all layers above.*

### 12.1 Compute

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Container Orchestration** | • Kubernetes cluster management • Pod scheduling & autoscaling • Multi-cluster orchestration • Cluster upgrades & lifecycle | EKS, GKE, AKS, OpenShift, Rancher |
| **Serverless Compute** | • Function-as-a-Service (FaaS) • Event-driven invocation • Cold start optimisation • Serverless application frameworks | AWS Lambda, Google Cloud Functions, Azure Functions, Knative |
| **Virtual Machines** | • VM provisioning & management • Image management & hardening • Auto-scaling groups • Spot/preemptible instance management | EC2, GCE, Azure VMs, Terraform-managed VMs |
| **Edge Compute** | • Edge function deployment • CDN-integrated compute • Low-latency edge processing • Edge configuration management | Cloudflare Workers, Lambda@Edge, Fastly Compute |

### 12.2 Data & Storage

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Relational Databases** | • Managed RDBMS provisioning • Read replica management • Automated backups & point-in-time recovery • Connection pooling & proxy | RDS, Cloud SQL, Aurora, Azure SQL, PlanetScale |
| **NoSQL Databases** | • Document, key-value, wide-column, graph databases • Auto-scaling & capacity management • Global replication • Consistency model selection | DynamoDB, MongoDB Atlas, Cassandra, CosmosDB, Neo4j |
| **Object Storage** | • Bucket management & lifecycle policies • Storage class tiering (hot/warm/cold/archive) • Cross-region replication • Versioning & soft delete | S3, GCS, Azure Blob Storage, MinIO |
| **Message Brokers & Streaming** | • Managed Kafka/Pulsar/NATS clusters • Partition & replication management • Consumer group orchestration • Broker monitoring & capacity planning | MSK, Confluent Cloud, Amazon Kinesis, Pub/Sub, NATS |

### 12.3 Networking

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Virtual Networking** | • VPC/VNet provisioning & management • Subnet design & IP address management • Peering & transit gateway configuration • Private link / service endpoints | AWS VPC, Azure VNet, GCP VPC, Terraform |
| **Load Balancing** | • L4/L7 load balancer management • SSL/TLS termination • Health check configuration • Global load balancing & failover | ALB/NLB, GCP Load Balancer, Azure Front Door, Envoy |
| **DNS Management** | • DNS zone & record management • Service-level DNS (internal resolution) • DNS-based traffic routing (weighted, geolocation) • DNS monitoring & DNSSEC | Route 53, Cloud DNS, Azure DNS, CoreDNS |
| **CDN & Edge Delivery** | • Static asset caching & delivery • Dynamic content acceleration • Cache invalidation policies • Edge security (WAF, bot protection) | CloudFront, Cloudflare, Fastly, Akamai |

### 12.4 Platform Resource Management

| Capability | Sub-Capabilities | Example Tooling |
|---|---|---|
| **Infrastructure-as-Code** | • Declarative infrastructure provisioning • State management & locking • Drift detection & remediation • Module/composition libraries | Terraform, Pulumi, Crossplane, AWS CDK, Bicep |
| **Resource Quotas & Governance** | • Namespace/project resource limits • Cloud account/subscription governance • Tag policy enforcement • Resource sprawl detection & cleanup | Kubernetes ResourceQuotas, AWS Service Control Policies, Azure Policy |
| **Multi-Cloud & Hybrid Management** | • Consistent tooling across cloud providers • Cross-cloud networking & identity • Workload portability • Cloud provider abstraction layers | Crossplane, Terraform multi-provider, Anthos, Azure Arc |

---

## 14. Feedback Flow Model

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                     WHO CONSUMES ANALYTICS                                   │
│                                                                              │
│  ┌─────────────────┐ ┌──────────────────┐ ┌──────────────────┐               │
│  │ Platform Product│ │ Domain Product   │ │ Enterprise       │               │
│  │ Management      │ │ Teams            │ │ Leadership       │               │
│  │ (SPOs, POs)     │ │ (Payments, CX,   │ │ (CTO, VP Eng,   │               │
│  │                 │ │  Lending, etc.)  │ │  CFO, CPO)       │               │
│  └────────┬────────┘ └────────┬─────────┘ └────────┬─────────┘               │
│           │                   │                     │                         │
│           │ "Is our golden    │ "What's our        │ "Are we getting         │
│           │  path adoption    │  deployment freq?   │  ROI on platform       │
│           │  at 80%?"         │  MTTR improving?"   │  investment?"          │
│           │                   │                     │                         │
└───────────┴───────────────────┴─────────────────────┴────────────────────────┘
                                │
                    ┌───────────▼───────────┐
                    │ STRATEGIC & AGILE     │◀── Analytics informs investment
                    │ PLANNING              │    decisions at all three tiers:
                    │                       │    Enterprise, Product, Technical
                    └───────────┬───────────┘
                                │
                    ┌───────────▼───────────┐
                    │ ENGINEERING &         │◀── Aggregates from ALL layers,
                    │ PRODUCT ANALYTICS     │    serves all consumers
                    └───────────┬───────────┘
                                │
                    ┌───────────▼───────────┐
                    │ ALL LAYERS BELOW      │──── Emit telemetry, events,
                    │ (SDLC, Platform,      │     and metrics upward
                    │  Operations, etc.)    │
                    └───────────────────────┘
```

### Feedback Destinations — Itemised

| Analytics Domain | Feeds Upward To | Example Insight |
|---|---|---|
| **Delivery & Engineering Analytics** | Enterprise Planning (portfolio velocity), Digital Product Planning (product delivery speed), Technical Planning (team bottlenecks) | "Lead time has increased 30% across the payments value stream — investigate CI/CD queue times" |
| **Product & Value Analytics** | Digital Product Planning (feature effectiveness), Enterprise Planning (product ROI) | "Feature X has 12% adoption after 6 weeks — consider pivot or deprecation" |
| **Developer Productivity & Experience** | Platform Product Management (platform effectiveness), Technical Planning (toil reduction priorities) | "Developer satisfaction with environment provisioning dropped from 4.2 to 3.1 �� investigate" |
| **Platform Analytics (self-analytics)** | Platform Product Management (capability investment), Enterprise Planning (platform ROI) | "Golden path template adoption is 78% — 22% of teams are building custom, investigate why" |
| **Quality & Security Analytics** | Enterprise Planning (risk posture), Digital Product Planning (product quality), Technical Planning (debt priorities) | "Payments product has 14 critical CVEs in dependencies — escalate to product planning" |
| **FinOps Analytics** | Enterprise Planning (budget allocation), Digital Product Planning (product cost), Technical Planning (cost-aware decisions) | "Cost per deployment increased 25% — linked to new observability data volume" |

---

## 15. Three Catalogs — How They Differ

```
┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│  DIGITAL PRODUCT CATALOG          "What business products do we     │
│  (Application & Portfolio Mgmt)    offer, and what systems power    │
│         │                          them?"                            │
│         │ composed of                                                │
│         ▼                                                            │
│  SOFTWARE SYSTEM CATALOG          "What software systems exist,     │
│  (Application & Portfolio Mgmt)    who owns them, and how do they   │
│         │                          relate?"                          │
│         │ built using                                                │
│         ▼                                                            │
│  PLATFORM SERVICE CATALOG         "What platform capabilities can   │
│  (Platform Int. & Delivery Svcs)   I self-service to build my       │
│                                    system?"                          │
└──────────────────────────────────────────────────────────────────────┘
```

| Catalog | Layer | Audience | Question It Answers |
|---|---|---|---|
| **Digital Product Catalog** | Application & Portfolio Mgmt | Product managers, engineering leadership, finance | *"What products do we run, what's their health, cost, and business value?"* |
| **Software System Catalog** | Application & Portfolio Mgmt | Engineering teams, architects, platform teams | *"What systems exist, who owns them, what do they depend on, are they healthy?"* |
| **Platform Service Catalog** | Platform Int. & Delivery Svcs | Developers | *"What can I provision right now to build my service?"* |

---

## 16. Layer Dependency Map

```
┌──────────────────────────┐
│  1. STRATEGIC & AGILE    │  Enterprise → Product → Technical planning
│     PLANNING             │
└────────────┬─────────────┘
             │◀── analytics & insights feed back up
             │
┌────────────▼─────────────┐
│  2. ENGINEERING &        │  Adoption, productivity, value, ROI,
│     PRODUCT ANALYTICS    │  health, maturity, executive reporting
└────────────┬─────────────┘
             │ insights inform
             ▼
┌──────────────────────────┐
│  3. DEVELOPER PLANE      │  IDE, agents, prototyping, SDLC phases
│     + SDLC Phases        │
└────────────┬─────────────┘
             │ consumes
             ▼
┌──────────────────────────┐
│  4. PLATFORM INTEGRATION │  APIs, data, events, delivery, config,
│     & DELIVERY SERVICES  │  self-service, extensibility, sandboxes
└────────────┬─────────────┘
             │ registered in & governed by
             ▼
┌──────────────────────────┐
│  5. APPLICATION &        │  System catalog, product catalog, lifecycle,
│     PORTFOLIO MGMT       │  dependencies, standards, tech audit
└────────────┬─────────────┘
             │ operational lifecycle managed by
             ▼
┌───────────────────��──────┐
│  6. SERVICE MANAGEMENT   │  Service catalog, change mgmt, incidents,
│     & INCIDENT MGMT      │  on-call, escalation, runbooks
└────────────┬─────────────┘
             │ informed by
             ▼
┌──────────────────────────┐
│  7. OBSERVABILITY &      │  Metrics, logs, traces, alerting, SLOs
│     MONITORING           │
└────────────┬─────────────┘
             │ monitors & instruments
             ▼
┌──────────────────────────┐
│  12. INFRASTRUCTURE &    │
│      RESOURCE SERVICES   │
└──────────────────────────┘

        ◀── CROSS-CUTTING (spans all layers) ──▶

 ┌────────────┐ ┌────────────┐ ┌────────────┐ ┌────────────┐ ┌────────────┐
 │ KNOWLEDGE  │ │ OSS        │ │ FINOPS     │ │ SECURITY   │ │ INFRA &    │
 │ MANAGEMENT │ │ GOVERNANCE │ │            │ │ SERVICES   │ │ RESOURCE   │
 │            │ │ & ENABLERS │ │            │ │            │ │ SERVICES   │
 └────────────┘ └────────────┘ └────────────┘ └────────────┘ └────────────┘
```

---

## 17. Product Ownership Structure

### Organisation Chart

```
Head of Product — Platform Engineering (1)
│
├── SPO 1 — Developer Experience & Planning (1)
│   ├── PO 1.1 — Planning & Collaboration (1)
│   ├── PO 1.2 — Developer Experience & Tooling (1)
│   ├── PO 1.3 — Engineering & Product Analytics (1)
│   ├── PS — Agentic & AI Tooling (1, shared)
│   ├── PS — Agile Practices & Tooling (1)
│   └── PS — Analytics & Data Engineering (1, shared)
│
├── SPO 2 — Platform Services & Delivery (1)
│   ├── PO 2.1 — Integration & Data Services (1)
│   ├── PO 2.2 — Delivery & Platform Experience (1)
│   ├── PO 2.3 — Application Portfolio & Standards (1)
│   ├── PS — Data & Event Architecture (1)
│   ├── PS — CI/CD & GitOps (1, shared)
│   └── PS — Developer Portal & Catalog (1, shared)
│
├── SPO 3 — Governance, Security & Compliance (1)
│   ├── PO 3.1 — Identity, Secrets & Access (1)
│   ├── PO 3.2 — AppSec, Supply Chain & OSS Gov. (1)
│   ├── PO 3.3 — Runtime Security & Compliance (1)
│   ├── PS — Supply Chain & SBOM (1, shared)
│   └── PS — Compliance & Audit (1, shared)
│
└── SPO 4 — Reliability & Operations (1)
    ├── PO 4.1 — Service & Incident Management (1)
    ├── PO 4.2 — Observability (1)
    ├── PO 4.3 — Infrastructure & Resources (1)
    ├── PO 4.4 — FinOps & Cost Governance (1)
    ├── PS — SRE Practices (1, shared)
    ├── PS — Cloud & Infrastructure (1, shared)
    └── PS — FinOps (1, shared)
```

### Headcount Summary

| Role | Count |
|---|---|
| Head of Product | 1 |
| Senior Product Owners | 4 |
| Product Owners | 12 |
| Product Specialists | 10 (several shared across POs) |
| **Total** | **27** |

### Ownership Map — Architecture Layer to Role

| Architecture Layer | SPO | Product Owners | Product Specialists |
|---|---|---|---|
| **Strategic & Agile Planning** | SPO 1 | PO 1.1 | PS Agile Practices |
| **Engineering & Product Analytics** | SPO 1 | PO 1.3 | PS Analytics & Data Engineering |
| **Developer Plane + SDLC** | SPO 1 | PO 1.2 | PS Agentic & AI |
| **Platform Int. & Delivery — Integration & Data** | SPO 2 | PO 2.1 | PS Data & Event, PS Cloud & Infra |
| **Platform Int. & Delivery — Delivery & Experience** | SPO 2 | PO 2.2 | PS CI/CD & GitOps, PS Developer Portal |
| **Application & Portfolio Management** | SPO 2 | PO 2.3 | PS Developer Portal |
| **Security — Identity, Secrets & Access** | SPO 3 | PO 3.1 | PS Compliance & Audit |
| **Security — AppSec, Supply Chain, OSS** | SPO 3 | PO 3.2 | PS Supply Chain & SBOM |
| **Security — Runtime & Compliance** | SPO 3 | PO 3.3 | PS Compliance & Audit |
| **Service Mgmt & Incident Mgmt** | SPO 4 | PO 4.1 | PS SRE Practices |
| **Observability & Monitoring** | SPO 4 | PO 4.2 | PS SRE Practices |
| **Infrastructure & Resource Services** | SPO 4 | PO 4.3 | PS Cloud & Infra |
| **FinOps** | SPO 4 | PO 4.4 | PS FinOps |
| **Knowledge Management** *(cross-cutting)* | SPO 1 (primary) | PO 1.1 (primary), all POs contribute | — |
| **Open Source Governance** *(cross-cutting)* | SPO 3 (primary) | PO 3.2 (primary) | PS Supply Chain & SBOM |

---

## 18. Mission Model: Secrets & Dependency Management Prioritisation

For a budget-constrained organisation needing to urgently address OSS package vulnerability exploits, two time-bound cross-cutting missions are recommended.

### Mission 1: Secrets Management Hardening

| Attribute | Detail |
|---|---|
| **Mission Sponsor** | Head of Product |
| **Mission Lead** | SPO 3 (Governance, Security & Compliance) |
| **Mission PO** | PO 3.1 (Identity, Secrets & Access) |
| **Contributing POs** | PO 2.1 (secrets injection), PO 2.2 (CI/CD secrets), PO 4.3 (Vault/KMS infra) |
| **Duration** | 12 weeks |

**Mission Backlog:**

| Priority | Initiative |
|---|---|
| **P0** | Audit all secrets: identify hardcoded, stale, and over-privileged secrets across all systems |
| **P0** | Enforce secrets injection via Vault/KMS — block env-var and config-file secrets in CI/CD |
| **P1** | Implement automated secrets rotation with zero-downtime for all Tier 1 systems |
| **P1** | Add secrets leak detection in pre-commit hooks and CI pipelines |
| **P2** | Implement workload identity (SPIFFE/SPIRE or cloud IAM) to reduce long-lived credentials |
| **P2** | Build secrets health dashboard with alerting on stale/unused secrets |
| **P3** | Self-service secrets provisioning in developer portal |

### Mission 2: Software Dependency & OSS Vulnerability Management

| Attribute | Detail |
|---|---|
| **Mission Sponsor** | Head of Product |
| **Mission Lead** | SPO 3 (Governance, Security & Compliance) |
| **Mission PO** | PO 3.2 (AppSec, Supply Chain & OSS Governance) |
| **Contributing POs** | PO 2.2 (CI/CD scanning), PO 2.3 (approved libraries), PO 1.2 (developer experience) |
| **Duration** | 16 weeks |

**Mission Backlog:**

| Priority | Initiative |
|---|---|
| **P0** | Generate SBOMs for all production artifacts and store in central registry |
| **P0** | Enable automated dependency scanning (Dependabot/Renovate + Snyk/Trivy) across all repos |
| **P0** | Implement CI/CD pipeline gate: block deployments with critical/high CVEs in dependencies |
| **P1** | Establish approved OSS library list with automated enforcement |
| **P1** | Implement OSS health scoring for consumed packages (OpenSSF Scorecard) |
| **P1** | Build developer-facing dependency dashboard in IDE and portal |
| **P2** | Implement license compliance scanning with policy enforcement |
| **P2** | Automated PR creation for dependency updates (Renovate/Dependabot with auto-merge for patch) |
| **P3** | Establish InnerSource program to reduce reliance on unmaintained external OSS |
| **P3** | Implement provenance attestation (SLSA Level 2+) for all build artifacts |

### Mission Governance

```
┌────────────────────────────────────────────────────────────────┐
│                  HEAD OF PRODUCT                                │
│                  (Mission Sponsor)                              │
│                                                                │
│  • Approves mission scope & budget                             │
│  • Resolves cross-SPO capacity conflicts                       │
│  • Weekly mission status review                                │
│  • Go/no-go for mission completion                             │
└───────────────────────┬────────────────────────────────────────┘
                        │
          ┌─────────────┴─────────────┐
          ▼                           ▼
┌──────────────────────┐   ┌──────────────────────┐
│ MISSION 1            │   │ MISSION 2            │
│ Secrets Hardening    │   │ Dependency & OSS     │
│ Lead: SPO 3          │   │ Vulnerability Mgmt   │
│ PO: PO 3.1           │   │ Lead: SPO 3          │
│ Duration: 12 weeks   │   │ PO: PO 3.2           │
│                      │   │ Duration: 16 weeks   │
│ Cadence:             │   │ Cadence:             │
│ • Weekly standup     │   │ • Weekly standup     │
│ • Bi-weekly demo     │   │ • Bi-weekly demo     │
│ • Monthly steering   │   │ • Monthly steering   │
└──────────────────────┘   └──────────────────────┘
```

---

## 19. Budget Allocation Model

```
┌──────────────────────────────────────────────────┐
│            TOTAL PLATFORM ENGINEERING BUDGET       │
│                                                    │
│  ┌────────────────────┐  60%                      │
│  │ BAU — Keep the     │  Ongoing platform          │
│  │ lights on +        │  maintenance, support,     │
│  │ incremental        │  and small improvements    │
│  │ improvement        │  across all POs            │
│  └────────────────────┘                            │
│                                                    │
│  ┌────────────────────┐  25%  ⚠️ REDIRECTED       │
│  │ MISSIONS —         │  Ring-fenced for the two   │
│  │ Secrets &          │  security missions         │
│  │ Dependency Mgmt    │  (temporary, 1–2 quarters) │
│  └────────────────────┘                            │
│                                                    │
│  ┌────────────────────┐  15%                      │
│  │ STRATEGIC —        │  Longer-term investments:  │
│  │ Platform evolution │  agentic platform, portal, │
│  │                    │  new capabilities          │
│  └────────────────────┘                            │
└──────────────────────────────────────────────────┘
```

**Post-mission rebalance:**

| Bucket | During Missions | Post-Missions |
|---|---|---|
| BAU | 60% | 55% |
| Missions | 25% | 10% (reserve) |
| Strategic | 15% | 35% |

---

## 20. Complete Layer Inventory Summary

| # | Layer | Type | Capability Groups | Purpose | Consumers |
|---|---|---|---|---|---|
| 1 | **Strategic & Agile Planning** | Top-level | 3 | Demand signals: enterprise OKRs → product roadmaps → sprint execution | All teams |
| 2 | **Engineering & Product Analytics** | Feedback loop | 7 (incl. shared infra) | Measure everything: adoption, productivity, value, ROI, health, maturity | Platform team, domain teams, leadership |
| 3 | **Developer Plane + SDLC** | Experience | 7 | Where developers work: IDE, agents, prototyping across Plan → Build → Deliver → Operate | All developers |
| 4 | **Platform Integration & Delivery Services** | Platform product | 7 | Self-service capabilities: APIs, data, events, delivery, config, sandboxes, extensibility | All developers |
| 5 | **Application & Portfolio Management** | Governance | 6 | Portfolio governance: system catalog, product catalog, lifecycle, tech audit, standards | Architects, platform team, leadership |
| 6 | **Service Management & Incident Management** | Operations | 4 | Operational lifecycle: ownership, change control, incidents, on-call | Operations, on-call teams |
| 7 | **Observability & Monitoring** | Signals | 5 | System visibility: metrics, logs, traces, alerting, SLOs | All teams |
| 8 | **Knowledge Management** | Cross-cutting | 6 | Organisational memory: docs, runbooks, onboarding, decisions, search | Everyone |
| 9 | **Open Source Governance & Enablers** | Cross-cutting | 6 | OSS lifecycle: licenses, SBOMs, InnerSource, health monitoring | Security, developers, legal |
| 10 | **FinOps** | Cross-cutting | 4 | Financial governance: visibility, metering, cross-charging, optimisation | Finance, leadership, all teams |
| 11 | **Security Services** | Cross-cutting | 4 | Protection: IAM, AppSec, supply chain, runtime | Security, all teams |
| 12 | **Infrastructure & Resource Services** | Cross-cutting | 4 | Foundational resources: compute, data, networking, resource management | Platform team |

---

*Document generated: 2026-04-16*
*Version: 1.0*
*Classification: Internal*
