# Development of AI-Based Startup Idea Validator with Market Analysis Assistance

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![Flask](https://img.shields.io/badge/Framework-Flask%203.x-black.svg)
![AI](https://img.shields.io/badge/AI-Groq%20LLM-green.svg)
![Database](https://img.shields.io/badge/Database-SQLite-lightgrey.svg)
![Frontend](https://img.shields.io/badge/Frontend-Bootstrap%205.3-purple.svg)
![Tests](https://img.shields.io/badge/Tests-128%20Offline%20Tests-success.svg)

An AI-powered startup idea validation and market analysis platform designed to help students, aspiring entrepreneurs, and first-time founders evaluate their startup ideas before investing time and money.

Built using Python Flask, Groq LLM, SQLite, web research services, and a multi-agent AI architecture.

The platform coordinates eight specialized AI agents to perform market research, competitor verification, SWOT analysis, risk assessment, MVP planning, Go-To-Market strategy, startup advisory, and report generation.

## Table of Contents

- Key Features
- System Architecture
- High-Level Multi-Tier Architecture
- Multi-Agent AI Validation Pipeline
- Web Research & Competitor Verification Pipeline
- Mathematical Models
- Database Entity Relationship Overview
- Technology Stack
- Quick Start Guide
- API Route Catalog
- Automated Testing & Quality Assurance
- Default System Credentials
- Project Directory Structure
- License

## Key Features

### 1. AI-Based Startup Idea Extraction

- **Idea Understanding:** Accepts startup ideas from users and identifies the main problem, proposed solution, industry, target customers, and key features.
- **Structured Idea Processing:** Converts user descriptions into structured information for further analysis.
- **Industry Flexibility:** Supports startup ideas across different industries, including EdTech, FinTech, HealthTech, Agriculture, SaaS, E-commerce, Logistics, and more.

### 2. Evidence-Based Market Research

- **Market Demand Analysis:** Examines market demand, industry trends, customer segments, and opportunities.
- **Web-Based Research:** Uses Tavily (optional), DuckDuckGo search, and other supported sources to collect relevant information.
- **Market Data Extraction:** Identifies available market-size figures and CAGR information from retrieved sources.
- **Source Verification:** Displays source references and links for available market information.
- **Evidence Classification:** Separates sourced information, AI analysis, AI assumptions, and computed values.
- **Insufficient Data Handling:** Displays an insufficient-data explanation when reliable market information is unavailable instead of presenting unsupported figures.

### 3. TAM, SAM & SOM Market Sizing Engine

- Calculates Total Addressable Market (TAM), Serviceable Available Market (SAM), and Serviceable Obtainable Market (SOM).
- Supports bottom-up and top-down market sizing methods.
- Uses AI-proposed assumptions with Python-based mathematical calculations.
- Provides low and high estimation scenarios.
- Displays formulas, assumptions, currency, and calculation details.
- Calculates individual market levels independently when sufficient information is available.

### 4. Verified Competitor Analysis

- **Competitor Identification:** Identifies potential direct, indirect, and emerging competitors.
- **Official Website Verification:** Checks competitor websites before including them as verified competitors.
- **Product and Feature Analysis:** Examines publicly available competitor products and features.
- **Pricing Analysis:** Displays pricing information when available from official sources.
- **Comparison Matrix:** Compares competitor offerings and positioning.
- **Market Gap Identification:** Highlights possible opportunities and differentiation areas.

### 5. SWOT Analysis & Risk Assessment

- Generates Strengths, Weaknesses, Opportunities, and Threats.
- Identifies technical, financial, market, operational, legal, and competitive risks.
- Evaluates each risk using impact and likelihood.
- Categorizes risks into High, Medium, and Low severity.
- Provides mitigation strategies and early-warning indicators.
- Separates source-based observations from AI-generated interpretations.

### 6. MVP Recommendation & Development Planning

- Identifies the essential features required for the first version of a startup product.
- Categorizes features into Must, Should, Could, and Deferred.
- Recommends development priorities and implementation order.
- Provides estimated development costs with assumptions.
- Suggests required resources, testing methods, and development timelines.
- Generates a practical product development roadmap.

### 7. Go-To-Market Strategy

- Recommends suitable business positioning and revenue models.
- Suggests pricing approaches using available competitor information.
- Provides customer acquisition and marketing strategies.
- Identifies possible first-customer segments.
- Generates customer interview questions and sample outreach messages.
- Provides a 30/60/90-day action plan.

### 8. AI-Based Startup Viability Scoring

- Calculates an overall startup viability score using five weighted evaluation dimensions.
- Evaluates market demand, competitive position, execution feasibility, business model, and risk resistance.
- Provides a written reason for each evaluation.
- Generates Proceed, Improve, and High Risk decision categories.
- Identifies factors reducing the score and possible improvement areas.
- Provides a confidence level based on available evidence and analysis.

### 9. AI Startup Advisor & Report Generation

- Provides an idea-specific AI chat advisor.
- Uses available market, competitor, SWOT, risk, and MVP analysis information to answer questions.
- Generates a consolidated startup validation report.
- Supports PDF, JSON, Markdown, and CSV exports.
- Maintains startup idea history.
- Supports comparison of previously analyzed ideas.

## System Architecture

### High-Level Multi-Tier Architecture

```text
+----------------------------------------------------------------+
|                    PRESENTATION LAYER                          |
|                                                                |
|  +--------------------+  +--------------------+                |
|  | User Authentication|  | Founder Dashboard  |                |
|  +--------------------+  +--------------------+                |
|                                                                |
|  +--------------------+  +--------------------+                |
|  | Idea Submission    |  | Analysis Pages     |                |
|  |                    |  | Market / Competitor|                |
|  |                    |  | SWOT / Risk / MVP   |                |
|  +--------------------+  +--------------------+                |
|                                                                |
|  +--------------------+  +--------------------+                |
|  | AI Startup Advisor |  | Reports & History  |                |
|  +--------------------+  +--------------------+                |
+-------------------------------+--------------------------------+
                                |
                         HTTP / JSON / AJAX
                                |
+-------------------------------v--------------------------------+
|                APPLICATION CONTROLLER LAYER                    |
|                                                                |
|                      Flask Application                         |
|                                                                |
|  Authentication | Dashboard | Idea Submission                 |
|  Analysis Routes | Chat APIs | History | Export                |
|  Settings | Error Handling | User Session Management          |
+-------------------------------+--------------------------------+
                                |
                                v
+----------------------------------------------------------------+
|               ORCHESTRATION & INTELLIGENCE LAYER               |
|                                                                |
|                    Pipeline Orchestrator                       |
|                                                                |
|  +------------------+       +------------------+               |
|  | Idea Extractor   |       | Market Analyzer  |               |
|  +------------------+       +------------------+               |
|                                                                |
|  +------------------+       +------------------+               |
|  | Competitor Agent |       | SWOT & Risk Agent|               |
|  +------------------+       +------------------+               |
|                                                                |
|  +------------------+       +------------------+               |
|  | MVP Recommender  |       | GTM Strategist   |               |
|  +------------------+       +------------------+               |
|                                                                |
|  +------------------+       +------------------+               |
|  | Startup Advisor  |       | Report Generator |               |
|  +------------------+       +------------------+               |
|                                                                |
|  Services: Groq | Search | Evidence | Sizing | Scoring         |
+-------------------------------+--------------------------------+
                                |
                                v
+----------------------------------------------------------------+
|                 PERSISTENCE & STORAGE LAYER                    |
|                                                                |
|                   SQLite Database                              |
|                                                                |
|  Users | Startup Ideas | Analysis Results                     |
|  Competitors | Chat Messages | Validation Reports              |
|                                                                |
|                   Generated Exports                            |
|                  PDF / JSON / CSV / Markdown                   |
+-------------------------------+--------------------------------+
                                |
                                v
+----------------------------------------------------------------+
|                    EXTERNAL SERVICES                           |
|                                                                |
|  Groq LLM API | Tavily Search (Optional)                       |
|  DuckDuckGo | Wikipedia | Official Competitor Websites         |
+----------------------------------------------------------------+
```

### Multi-Agent AI Validation Pipeline

The application uses eight specialized agents coordinated by a central pipeline orchestrator.

```text
                 STARTUP IDEA SUBMISSION
                           |
                           v
                 +-------------------+
                 |   IDEA EXTRACTOR  |
                 |      Stage 1     |
                 +-------------------+
                           |
                           v
                 STRUCTURED IDEA DATA
                           |
              +------------+------------+
              |                         |
              v                         v
      +----------------+       +------------------+
      | MARKET ANALYZER|       | COMPETITOR AGENT |
      |    Stage 2     |       |     Stage 2      |
      +----------------+       +------------------+
              |                         |
              +------------+------------+
                           |
                           v
                   ANALYSIS CONTEXT
                           |
          +----------------+----------------+
          |                |                |
          v                v                v
   +--------------+  +--------------+  +--------------+
   | SWOT & RISK  |  |     MVP      |  |     GTM      |
   |    Agent     |  | Recommender  |  |  Strategist  |
   |   Stage 3    |  |   Stage 3    |  |   Stage 3    |
   +--------------+  +--------------+  +--------------+
          |                |                |
          +----------------+----------------+
                           |
                           v
                  CONSOLIDATED RESULTS
                           |
                 +---------+---------+
                 |                   |
                 v                   v
        +----------------+  +------------------+
        | STARTUP ADVISOR|  | REPORT GENERATOR |
        |    Stage 4     |  |     Stage 4      |
        +----------------+  +------------------+
                 |                   |
                 +---------+---------+
                           |
                           v
                FINAL VALIDATION REPORT
                           |
                           v
              VIABILITY SCORE & VERDICT
                           |
                           v
                    REPORT EXPORT
```

**Execution Workflow:**

- Stage 1: The Idea Extractor structures the submitted startup idea and prepares relevant search queries.
- Stage 2: Market Analyzer and Competitor Agent perform independent research tasks in parallel.
- Stage 3: SWOT and Risk Agent, MVP Recommender, and GTM Strategist perform their analysis tasks in parallel.
- Stage 4: Startup Advisor and Report Generator prepare recommendations and the final report.

The pipeline uses parallel execution for independent tasks. Quick mode can skip the advisor brief to reduce processing work.

### Web Research & Competitor Verification Pipeline

```text
                 STRUCTURED STARTUP IDEA
                           |
                           v
                   SEARCH QUERY GENERATION
                           |
                           v
              +------------+-------------+
              |            |             |
              v            v             v
           Tavily      DuckDuckGo     Wikipedia
          (Optional)    Search        Background
              |            |             |
              +------------+-------------+
                           |
                           v
                  SOURCE NORMALIZATION
                           |
                           v
              SOURCE IDS & RELIABILITY DATA
                           |
                           v
             MARKET FIGURE AND CAGR EXTRACTION
                           |
                           v
               CANDIDATE COMPETITOR IDENTIFICATION
                           |
                           v
                 RELEVANCE EVALUATION
                           |
                           v
                OFFICIAL WEBSITE VERIFICATION
                           |
                           v
             PRODUCT / FEATURES / PRICING CHECK
                           |
                           v
                 VERIFIED RESEARCH RESULTS
                           |
                           v
                 MARKET & COMPETITOR ANALYSIS
```

The research pipeline collects available information, processes retrieved sources, and separates verified information from AI-generated analysis.

Competitors are included as verified competitors only after the supported website verification process. Unverified candidates are excluded from verified competitor results.

## Mathematical Models

### 1. TAM, SAM & SOM Market Sizing

**Bottom-Up Market Sizing**

```text
TAM = Customers × Annual Revenue per Customer

SAM = TAM × Reachable Market Share

SOM = SAM × Realistic Market Entry Share
```

**Top-Down Market Sizing**

```text
TAM = Published Market Size from a Retrieved Source

SAM = TAM × Share of Market the Product Can Serve

SOM = SAM × Realistic Market Entry Share
```

The system uses available source information and assumptions to calculate low and high estimates. A market level is marked as insufficient data when a responsible calculation is not possible.

### 2. Startup Viability Scoring Model

The application uses five weighted evaluation dimensions.

| Evaluation Dimension | Weight |
|---|---:|
| Market Demand | 25% |
| Competitive Position | 20% |
| Execution Feasibility | 20% |
| Business Model | 15% |
| Risk Resistance | 20% |
| **Total** | **100%** |

**Viability Score Formula**

```text
Viability Score =
(0.25 × Market Demand)
+ (0.20 × Competitive Position)
+ (0.20 × Execution Feasibility)
+ (0.15 × Business Model)
+ (0.20 × Risk Resistance)
```

Each dimension is evaluated using ratings from 1 to 5 and converted into a percentage.

When a dimension cannot be reliably scored, it is excluded and the remaining weights are normalized. At least three dimensions must be scorable.

When sourced market data is unavailable, the Market Demand score is capped at 70%.

### 3. Viability Decision Categories

| Risk Category | Score Range | Description |
|---|---:|---|
| PROCEED | 75–100 | The idea shows stronger potential based on the available analysis. |
| IMPROVE | 55–74 | The idea needs further improvement. |
| HIGH RISK | Below 55 | Significant challenges require attention. |

### 4. Risk Assessment Mathematical Model

```text
Risk Points = Impact × Likelihood
```

Impact and likelihood are each rated from 1 to 10.

**Risk Severity Classification**

| Severity | Risk Points |
|---|---:|
| High | 56 and above |
| Medium | 30–55 |
| Low | Below 30 |

**Composite Risk Calculation**

```text
Composite Risk =
(0.6 × Average of Top 3 Risk Scores)
+
(0.4 × Average of All Risk Scores)
```

**Risk Resistance**

```text
Risk Resistance = 100 - Composite Risk
```

The risk resistance value contributes to the overall viability score.

## Database Entity Relationship Overview

The application uses SQLite3 for storing user accounts, startup ideas, analysis results, competitors, conversations, and validation reports.

```text
+-------------------+
|       USERS       |
+-------------------+
| user_id (PK)      |
| name              |
| email             |
| password_hash     |
+-------------------+
          |
          | 1
          |
          | Many
          v
+-------------------+
|   STARTUP IDEAS   |
+-------------------+
| idea_id (PK)      |
| user_id (FK)      |
| title             |
| industry          |
| description       |
+-------------------+
          |
          +--------------------+
          |                    |
          v                    v
+-------------------+  +-------------------+
| ANALYSIS RESULTS  |  |    COMPETITORS    |
+-------------------+  +-------------------+
| result_id (PK)    |  | competitor_id     |
| idea_id (FK)      |  | idea_id (FK)      |
| analysis_data     |  | name              |
+-------------------+  +-------------------+
          |
          +--------------------+
          |                    |
          v                    v
+-------------------+  +-------------------+
|  CHAT MESSAGES    |  | VALIDATION REPORTS|
+-------------------+  +-------------------+
| message_id        |  | report_id (PK)    |
| idea_id (FK)      |  | idea_id (FK)      |
| message           |  | report_data       |
+-------------------+  +-------------------+
```

*This is a logical relationship overview. Refer to the database models for the exact implementation and schema.*

## Technology Stack

**Backend Framework:** Python 3.10+, Flask 3.x, Jinja2, Flask-Login, Werkzeug Password Hashing, python-dotenv.

**AI & Language Models:** Groq Chat Completions API, `openai/gpt-oss-120b` default model, `openai/gpt-oss-20b` fallback model.

**Web Research:** Tavily (optional), DDGS / DuckDuckGo Search, Wikipedia, Requests.

**Evidence & Data Processing:** BeautifulSoup4, lxml, Regular Expressions.

**Database Engine:** SQLite3 with database connection management.

**Frontend Architecture:** HTML5, CSS3, Vanilla JavaScript, Bootstrap 5.3, Bootstrap Icons, Chart.js 4.

**Report Generation:** ReportLab (PDF), JSON, Markdown, CSV.

**Concurrency:** Python `concurrent.futures.ThreadPoolExecutor`, threading.

**Testing & Quality Assurance:** Python unittest (128 offline automated tests).

## Quick Start Guide

### 1. Clone the Repository

```bash
git clone https://github.com/varsh120925-cmd/AI-Startup-Idea-Validator.git
cd AI-Startup-Idea-Validator
```

### 2. Set Up Virtual Environment

**On Windows:**

```powershell
python -m venv venv
venv\Scripts\activate
```

**On macOS/Linux:**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file using `.env.example` as a reference.

Configure the following:

```env
FLASK_SECRET_KEY=your_secret_key
GROQ_API_KEY=your_groq_api_key
TAVILY_API_KEY=your_tavily_api_key
```

- `GROQ_API_KEY` is required for AI analysis.
- `TAVILY_API_KEY` is optional when using the supported alternative search services.
- Keep your actual `.env` file private.

### 5. Run the Application

```bash
python scripts/diagnose.py
python run.py
```

Open your browser and navigate to:

```text
http://127.0.0.1:5000
```

## API Route Catalog

| Method | Endpoint | Description | Access |
|---|---|---|---|
| GET | `/` | Landing page | Public |
| GET / POST | `/login` | User login | Public |
| GET / POST | `/register` | User registration | Public |
| GET | `/demo-login` | Demo account login | Public |
| GET | `/logout` | End user session | Authenticated |
| GET | `/dashboard` | Founder validation dashboard | Authenticated |
| GET / POST | `/submit` | Submit startup idea | Authenticated |
| GET | `/history` | Browse and compare previous ideas | Authenticated |
| GET | `/advisor` | General startup advisor | Authenticated |
| GET | `/idea/<id>/market` | Market analysis and TAM/SAM/SOM | Idea Owner |
| GET | `/idea/<id>/competitors` | Competitor analysis | Idea Owner |
| GET | `/idea/<id>/swot` | SWOT analysis | Idea Owner |
| GET | `/idea/<id>/risks` | Risk assessment | Idea Owner |
| GET | `/idea/<id>/mvp` | MVP recommendations | Idea Owner |
| GET | `/idea/<id>/gtm` | Go-To-Market strategy | Idea Owner |
| GET | `/idea/<id>/report` | Final validation report | Idea Owner |
| GET | `/idea/<id>/chat` | Idea-specific advisor chat | Idea Owner |
| POST | `/api/idea/<id>/run` | Start or rerun validation pipeline | Idea Owner |
| GET | `/api/idea/<id>/status` | Check pipeline progress | Idea Owner |
| POST | `/api/idea/<id>/chat` | Send advisor message | Idea Owner |
| POST | `/api/idea/<id>/chat/clear` | Clear advisor conversation | Idea Owner |
| POST | `/api/idea/<id>/delete` | Delete idea and results | Idea Owner |
| GET | `/api/export/<id>/pdf` | Download PDF report | Idea Owner |
| GET | `/api/export/<id>/json` | Download JSON report | Idea Owner |
| GET | `/api/export/<id>/markdown` | Download Markdown report | Idea Owner |
| GET | `/api/export/<id>/csv` | Download CSV report | Idea Owner |
| GET | `/api/ideas/compare` | Compare startup ideas | Authenticated |
| GET / POST | `/settings` | User and application settings | Authenticated |
| GET | `/api/settings/test-groq` | Test Groq connection | Authenticated |
| GET | `/api/settings/test-tavily` | Test Tavily connection | Authenticated |
| POST | `/api/sample/load` | Load sample startup ideas | Authenticated |

## Automated Testing & Quality Assurance

Run the automated test suite using Python unittest:

```bash
python -m unittest discover -s tests
```

Alternatively:

```bash
python tests/run_all_tests.py
```

**Offline Test Suite: 128 Tests**

The test suite covers core functionality, scoring, database operations, agents, orchestration, application routes, and PDF generation.

| Test Module | Test Count |
|---|---:|
| `test_core.py` | 32 |
| `test_sizing_fix.py` | 22 |
| `test_app.py` | 16 |
| `test_pipeline.py` | 15 |
| `test_improvements.py` | 15 |
| `test_agents.py` | 9 |
| `test_routes.py` | 9 |
| `test_any_idea.py` | 4 |
| `test_db.py` | 3 |
| `test_orchestrator.py` | 2 |
| `test_pdf.py` | 1 |
| **Total** | **128** |

The offline tests use fake LLM and search services to validate application logic without requiring live external API calls.

For additional live research-quality checks:

```bash
python scripts/verify_three_ideas.py
```

Use the following command to check additional industries:

```bash
python scripts/verify_three_ideas.py --all
```

## Default System Credentials

| Role | Email Address | Password | Landing Portal |
|---|---|---|---|
| Demo User | `demo@startupvalidator.com` | `password123` | Dashboard (`/dashboard`) |

**Security Note:** These credentials are for local demonstration only. Change or remove default credentials before public deployment.

## Project Directory Structure

```text
startup-idea-validator-ai/
│
├── agents/                         # Specialized AI Agents
│   ├── base_agent.py              # Base Agent Functionality
│   ├── idea_extractor.py          # Startup Idea Extraction
│   ├── market_analyzer.py         # Market Research & Sizing
│   ├── competitor_agent.py        # Competitor Verification
│   ├── swot_risk_agent.py         # SWOT & Risk Analysis
│   ├── mvp_recommender.py         # MVP Recommendations
│   ├── gtm_strategist.py          # Go-To-Market Strategy
│   ├── startup_advisor.py         # AI Startup Advisor
│   └── report_generator.py        # Final Report Generation
│
├── orchestration/                  # Multi-Agent Pipeline
│   ├── pipeline.py                # Agent Execution Orchestrator
│   └── context_store.py           # Shared Analysis Context
│
├── services/                       # Supporting Services
│   ├── groq_service.py             # Groq LLM Integration
│   ├── search_service.py           # Web Search Integration
│   ├── evidence.py                 # Evidence Processing
│   ├── sizing.py                   # TAM/SAM/SOM Calculations
│   ├── scoring.py                  # Viability & Risk Scoring
│   ├── quality.py                  # Analysis Quality Checks
│   └── pdf_service.py              # PDF Report Generation
│
├── database/                       # Database Management
│   ├── db.py                       # SQLite Connection Management
│   └── models.py                   # Database Models
│
├── templates/                      # HTML Templates
│   ├── auth/                       # Login & Registration
│   ├── dashboard/                  # Dashboard & Analysis Pages
│   ├── partials/                   # Reusable Template Components
│   ├── base.html                   # Base Template
│   └── error.html                  # Error Page
│
├── static/                         # Frontend Assets
│   ├── css/                        # Stylesheets
│   ├── js/                         # JavaScript Files
│   └── img/                        # Images & Icons
│
├── tests/                          # Automated Test Suite
│   ├── fakes.py                    # Fake LLM & Search Services
│   └── test files                  # Unit & Integration Tests
│
├── scripts/                        # Utility Scripts
│   ├── diagnose.py                 # System Diagnostics
│   └── verify_three_ideas.py       # Live Research Verification
│
├── docs/                           # Project Documentation
│   └── Team_Viva_Guide.pdf         # Supporting Project Documentation
│
├── exports/                        # Generated Reports
│
├── app.py                          # Flask Application
├── config.py                       # Application Configuration
├── run.py                          # Application Entry Point
├── requirements.txt                # Python Dependencies
├── .env.example                    # Environment Configuration Template
├── .gitignore                      # Git Ignore Rules
└── README.md                       # Project Documentation
```

## License

Refer to the `LICENSE` file in the repository for the applicable license terms.
