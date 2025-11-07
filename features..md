# Trade Store Features

## Assumptions
- Features cover OTC Derivatives product set (Rates, Credit, Equity)
- Structured Notes - additional requirements not covered here.
- No ‘traditional’ position management

## Data Platform
- Define Trade model (generic deal level attributes)
- Define Instrument model (potentially Quant-owned, product specific)
- Implement data persistence (define transaction boundaries)
- Versioning and Audit Trail
- Implement queryable data structure, potentially caching, based on fast access requirements (eg. real time risk management)
- Implement a reporting sub-system for more batch based, user self-service or complex analytic queries.
- Implement replication or sharding across geographical locations.  Consider regional data protection compliance, potentially segregation/sharding of counterparty.
- Implement data archiving (legal/data retention requirements).

## Services Implementation
- Ticketing service - control plane to allocate trace/workflow ids, monitor for workflow exceptions, facilitate replay.  Supports choreography of other event based services.
- Adaptors from vendor platforms (translation from raw lifecycle events to canonical model)
- Reference Data sourcing
- Orchestration of booking, STP, Clearing and distribution workflows
- Booking Services
- Query Services
- Publisher Services
- API Gateway - authentication, load-balancing, rate-limiting etc
- Logging & Monitoring

## Booking Service Capabilities
- Authentication and Authorisation (Entitlement Validation)
- State Transition Workflow - incl support for Draft/Scenario, restore
- Approval Process Workflow
- Validation & Enrichment of Core Trade attributes
- Validation & Enrichment of Instrument
- Enrichment for Trade/Product Labelling eg. ISDA Taxonomy
- Enrichment of Reg Reporting attributes (ISIN, USI/UTI, Execution TS, etc)
- Determination of Clearing Eligibility / MAT etc
- Legal Linkage Key Enrichment
- Sales Revenue Enrichment
- Switch Ticketing (enforced with exceptions): Back to Back, Interbook, Intercompany
- Structure Trade Capture
- Bulk Booking (Import from file, Managed Exceptions)
- Pricer Integration

## Distribution
- Publication Routing Rules invoked on each Lifecycle Event
- Pragmatically, a transformation for different downstream requirements.
- High performance cache query for notification / call back.

## Lifecycle

### Trade Capture / Amendments
- New Trade
- Amendment
- Cancel
- Novation (Full/Partial)
- Compression
- Structured Trade Capture (multi-leg, multi-system)

### Scheduled Lifecycle Events
- Cashflow Calculation & Generation (Coupons, premiums, interest)
- Trade-Related Payments (Fees, Upfronts, Amendments, Adjustments)
- Floating Rate Resets
- Fixings (Equity, FX, Commodity)
- Dividend / Corporate Action Adjustments
- Swaption Exercise (European-style)
- Maturity (Final settlement)
- Rolls
- Scheduled Amortizations / Corrections (e.g. Asset-Backed CDS)
- Mortgage Credit Floating Payments

### Unscheduled Lifecycle Events
- Early / Full Termination
- Partial Termination / Unwind
- Break Clauses
- Swaption Exercise (American/Bermudan)
- Barrier Events (Knock-in / Knock-out)
- Call / Put Events (Embedded options)
- Credit Events (CDS triggers)
- Operational Events
- Allocations
- Clearing Submissions / Status Updates
- Legal Linkage / CSA Updates
- Trade Enrichment / Corrections
- 871M Tax Reassessments
- Regulatory Reporting (EMIR, CFTC, MiFID II)

### Reference Data Integration
- Counterparty
- Book / Desk Hierarchy
- Trader / Marketer / Broker
- Instrument & Product Definitions (e.g. Bonds, Swaps, Options, Indices)
- Legal Agreements & CSA Collateral Terms
- Credit Reference Entities / Obligations / RED (Reference Entity Database) Codes
- Index Data (Floating Rate Indices, Inflation Indices, Benchmarks)
- Calendars & Business Day Conventions
- Currency / FX Rate Conventions

### Straight Through Processing / Vendor Platform Integration
- For ICELink (Credit) and MarkitWire (Credit/Rates/EQD)
- Clearing Houses (CCIL, CME Group, Eurex Clearing, ICE Clear, LCH, JSCC, KRX)
- Dealer to Client / Dealer to Dealer
- Swap Execution Facility (SEF)
- Bi-directional workflows for
  - Execution
  - Affirmation
  - Clearing
  - Novations
  - Unwinds

### Controls
- Exception Management
- Unapproved / Late trades
- Pending Clearing
- FOBO Reconciliation 
- DTCC Reconciliation

### IT Support Tooling
- Manage Exceptions (STP, Message Routing)
- Configuration updates

### Downstream Integration
- Publication Routing Rules evaluation on each lifecycle event
- Trading Risk
- Market Risk
- Credit Risk
- External Validation / Confirmation
- Reg Reporting
- Legal & Compliance
- Sales & RMs
- Settlement
- Accounting & Finance




