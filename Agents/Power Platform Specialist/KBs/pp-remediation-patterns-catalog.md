---
title: Power Platform Remediation Patterns
document_type: RemediationPatterns
domain: LowCode
product_family: Microsoft Power Platform

owner: Low Code Team
version: 2.0.0
status: Approved
review_date: 2027-06-15

audience:
  - Solution Architect
  - Developer
  - Support Engineer
  - Platform Administrator

tags:
  - performance
  - reliability
  - security
  - automation
  - agents
  - alm
  - remediation
  - optimization
  - troubleshooting
  - scalability

related_documents:
  - docs/power-platform/pp-performance-causes-catalog.md
---
<!-- markdownlint-disable MD024 MD025 -->

# Power Platform Remediation Patterns

## Purpose

This document defines reusable corrective-action patterns for diagnosing and resolving performance, reliability, security, automation, agent, and application lifecycle management (ALM) issues in Power Platform solutions.

Each remediation pattern includes:

- Applies To
- When to Apply
- Recommended Actions
- Why It Helps

Use these patterns as building blocks when designing corrective actions for identified causes. Select the smallest pattern or combination that addresses the validated failure mode; do not treat a pattern as a substitute for diagnosis.

## Remediation Patterns Catalog

### RP01 — Reduce Data Volume

#### Applies To

- Canvas Apps
- Power Automate
- SharePoint Lists
- Dataverse
- Large Datasets

#### When to Apply

- Large datasets
- Slow queries
- Slow filtering operations
- Full dataset retrieval before filtering

#### Recommended Actions

- Apply filters at the source before retrieving data
- Limit results to records required for the current task
- Use indexed columns where applicable
- Use pre-filtered views where applicable

#### Why It Helps

- Reduces data transferred to the client
- Improves load time
- Improves responsiveness

#### Related Causes

- C01 — Non-Delegable Query on Large Dataset
- C02 — Excessive Data Loading at App Start
- C03 — Large Dataset Without Data Shaping or Pagination
- C07 — Inefficient Query or Filter Design in Flows or Data Access

---

### RP02 — Push Processing to the Data Source

#### Applies To

- Canvas Apps
- Dataverse
- Delegation Scenarios
- Data Retrieval Operations

#### When to Apply

- Delegation warnings are present
- Filtering is executed client-side
- Logic is executed client-side
- Performance degrades as datasets grow

#### Recommended Actions

- Use delegable functions
- Execute filtering at the data source
- Execute sorting at the data source
- Avoid post-retrieval processing

#### Why It Helps

- Leverages backend execution
- Improves scalability
- Improves result accuracy

#### Related Causes

- C01 — Non-Delegable Query on Large Dataset
- C03 — Large Dataset Without Data Shaping or Pagination
- C07 — Inefficient Query or Filter Design in Flows or Data Access

### RP03 — Replace Non-Scalable Patterns

#### Applies To

- Canvas Apps
- Formula Design
- Data Retrieval Logic

#### When to Apply

- Solution works with small datasets but not at scale
- Performance degrades as data grows

#### Recommended Actions

- Remove full dataset collection patterns
- Replace non-delegable formulas
- Avoid repeated full data reloads

#### Why It Helps

- Prevents exponential performance degradation

#### Related Causes

- C01 — Non-Delegable Query on Large Dataset
- C03 — Large Dataset Without Data Shaping or Pagination

### RP04 — Defer Non-Essential Processing

#### Applies To

- Canvas Apps
- Startup Logic
- Screen Initialization

#### When to Apply

- Slow app startup
- Slow screen loads
- Heavy OnStart processing
- Heavy OnVisible processing

#### Recommended Actions

- Move non-critical logic out of startup events
- Load data on demand
- Trigger operations through user actions where appropriate

#### Why It Helps

- Improves perceived performance
- Reduces initial load times

#### Related Causes

- C02 — Excessive Data Loading at App Start
- C03 — Large Dataset Without Data Shaping or Pagination

---

### RP05 — Limit Data Payload

#### Applies To

- Canvas Apps
- Data Retrieval
- Lists
- Dataverse

#### When to Apply

- Slow retrieval operations
- Slow rendering operations
- Excessive fields
- Large attachments
- Large images

#### Recommended Actions

- Retrieve only required columns
- Avoid loading heavy fields unless necessary
- Preserve Explicit Column Selection behavior
- Use ShowColumns() only when column lineage is lost

#### Why It Helps

- Reduces network overhead
- Improves rendering performance

#### Related Causes

- C01 — Non-Delegable Query on Large Dataset
- C02 — Excessive Data Loading at App Start
- C03 — Large Dataset Without Data Shaping or Pagination

### RP06 — Simplify Execution Logic

#### Applies To

- Canvas Apps
- Power Automate
- Formulas
- Business Logic

#### When to Apply

- Complex formulas
- Nested conditions
- Computation-related performance issues

#### Recommended Actions

- Break formulas into smaller reusable parts
- Remove repeated calculations
- Remove excessive nesting
- Use named formulas where appropriate

#### Why It Helps

- Reduces computation cost
- Improves maintainability

#### Related Causes

- C04 — Monolithic App or Flow Design
- C11 — Poor Reuse or Component Strategy Leading to Repeated Heavy Logic

### RP07 — Control Execution Frequency

#### Applies To

- Canvas Apps
- Data Refresh Operations
- Runtime Processing

#### When to Apply

- Repeated refresh operations
- Repeated recalculations
- Logic executes more frequently than necessary

#### Recommended Actions

- Avoid reloading data on every navigation event
- Refresh data only when needed
- Cache results where appropriate

#### Why It Helps

- Reduces redundant operations
- Improves responsiveness

#### Related Causes

- C02 — Excessive Data Loading at App Start
- C03 — Large Dataset Without Data Shaping or Pagination

### RP08 — Optimize UI Rendering

#### Applies To

- Canvas Apps
- Galleries
- Screens
- User Interface Components

#### When to Apply

- UI responsiveness issues
- Heavy galleries
- Heavy screens

#### Recommended Actions

- Reduce number of rendered controls
- Avoid expensive formulas per item
- Load detail content only when needed

#### Why It Helps

- Improves rendering speed
- Improves usability

#### Related Causes

- C02 — Excessive Data Loading at App Start
- C03 — Large Dataset Without Data Shaping or Pagination

### RP09 — Isolate the Bottleneck

#### Applies To

- Canvas Apps
- Power Automate
- Troubleshooting Activities

#### When to Apply

- Root cause is unclear
- Multiple factors may contribute to slowness

#### Recommended Actions

- Identify the slowest component
- Temporarily disable logic to isolate impact
- Use Monitor or telemetry tools for analysis

#### Why It Helps

- Enables accurate diagnosis
- Prevents incorrect remediation efforts

#### Related Causes

- All Performance Causes

### RP10 — Restructure Solution Architecture

#### Applies To

- Canvas Apps
- Power Automate
- Solution Architecture

#### When to Apply

- Performance issues are systemic
- Local optimizations are insufficient

#### Recommended Actions

- Split large apps into modular components
- Split large flows into modular components
- Separate UI logic from background processing
- Re-evaluate data platform choices

#### Why It Helps

- Enables long-term scalability
- Enables long-term maintainability

#### Related Causes

- C04 — Monolithic App or Flow Design
- C05 — Incorrect Tool or Component Used for the Workload
- C06 — Long-Running Synchronous Process Instead of Asynchronous Design
- C13 — Datastore Choice Not Aligned with Solution Needs

### RP11 — Apply Configuration or Governance Fixes

#### Applies To

- Environments
- Connectors
- Governance Controls
- Platform Configuration

#### When to Apply

- Performance is impacted by configuration
- Performance is impacted by environment settings

#### Recommended Actions

- Validate indexed columns
- Review data structure
- Review connector configuration
- Review environment setup
- Align governance policies with usage patterns

#### Why It Helps

- Eliminates hidden bottlenecks
- Improves operational stability

#### Related Causes

- C12 — Missing or Weak Monitoring for Degraded Performance
- C13 — Datastore Choice Not Aligned with Solution Needs

### RP12 — Validate Improvements with Metrics

#### Applies To

- Performance Optimization Efforts
- Post-Remediation Validation

#### When to Apply

- After performance fixes have been implemented

#### Recommended Actions

- Compare before-and-after performance metrics
- Use Monitor or analytics tools
- Confirm removal of delegation warnings
- Validate response-time improvements

#### Why It Helps

- Confirms remediation effectiveness
- Prevents regression

#### Related Causes

- C12 — Missing or Weak Monitoring for Degraded Performance

### RP13 — Handle Throttling and Transient Failures

#### Applies To

- Power Automate
- Dataverse
- Connectors
- Integrations

#### When to Apply

- HTTP 429 responses
- Intermittent connector or service failures
- Request limits or burst traffic

#### Recommended Actions

- Use bounded retry policies and honor `Retry-After` guidance
- Reduce burst traffic with filtering, batching, pacing, or queues
- Split oversized loops and record the failed operation for replay
- Define a terminal failure path for exhausted retries

#### Why It Helps

- Prevents transient faults from becoming permanent failures
- Reduces pressure on protected services
- Makes recovery observable and repeatable

#### Related Causes

- C06 — Long-Running Synchronous Process Instead of Asynchronous Design
- C07 — Inefficient Query or Filter Design in Flows or Data Access
- C14 — Throttling or Transient Service Limits

---

### RP14 — Constrain Trigger Scope and Ensure Idempotent Processing

#### Applies To

- Power Automate cloud flows
- Event-driven integrations
- High-volume record processing

#### When to Apply

- A flow triggers unexpectedly or multiple times
- A flow updates the record that triggers it
- Duplicate actions or parallel conflicts occur

#### Recommended Actions

- Add precise trigger conditions and event filters
- Use a correlation or processed flag to prevent self-triggering
- Make writes idempotent and use stable business keys
- Configure concurrency deliberately and remove duplicate flows

#### Why It Helps

- Prevents duplicate processing and infinite loops
- Reduces unnecessary requests and conflicting updates

#### Related Causes

- C09 — Misused Parallelism or Unsafe Concurrency
- C15 — Trigger Scope or Duplicate Processing

---

### RP15 — Design Efficient Dataflow ETL

#### Applies To

- Power Query
- Dataflows
- Dataverse
- Data warehouses

#### When to Apply

- Refreshes are slow or unreliable
- Large datasets are transformed repeatedly
- Downstream data is delayed

#### Recommended Actions

- Filter and select columns at the source
- Push foldable transformations upstream where supported
- Use incremental refresh or watermark-based extraction
- Separate extraction, transformation, and loading stages when useful

#### Why It Helps

- Reduces refresh volume and transformation cost
- Improves repeatability and data availability

#### Related Causes

- C03 — Large Dataset Without Data Shaping or Pagination
- C08 — Inefficient Power Query or Dataflow Transformations
- C15 — Trigger Scope or Duplicate Processing

---

### RP16 — Validate at Production Scale

#### Applies To

- Canvas Apps
- Power Automate
- Dataverse
- Power Pages
- Dataflows

#### When to Apply

- A solution works in development but fails under realistic volume or concurrency
- A change is approaching production release

#### Recommended Actions

- Test production-like row counts, payloads, users, and event rates
- Exercise peak and sustained workloads separately
- Capture response times, failure rates, request usage, and throughput
- Record acceptance thresholds and retest after material changes

#### Why It Helps

- Exposes scale bottlenecks before release
- Distinguishes capacity problems from functional defects

#### Related Causes

- C01 — Non-Delegable Query on Large Dataset
- C03 — Large Dataset Without Data Shaping or Pagination
- C08 — Inefficient Power Query or Dataflow Transformations
- C10 — Lack of Scale Testing Before Production

---

### RP17 — Validate Inputs and Handle Failures Defensively

#### Applies To

- Power Automate
- Canvas Apps
- Connectors
- Dataverse operations

#### When to Apply

- Actions fail on null, malformed, or unexpected values
- A flow has weak error handling or unclear failure outcomes

#### Recommended Actions

- Validate required fields and schemas before connector calls
- Use explicit conditions and null-coalescing defaults where appropriate
- Add scopes, Configure Run After paths, and actionable notifications
- Preserve correlation IDs and failed inputs for diagnosis or replay

#### Why It Helps

- Converts opaque runtime errors into controlled outcomes
- Prevents bad inputs from propagating through a process

#### Related Causes

- C06 — Long-Running Synchronous Process Instead of Asynchronous Design
- C16 — Missing Validation or Failure Handling

---

### RP18 — Correct Identity, Access, Licensing, and Policy Configuration

#### Applies To

- Power Apps
- Power Automate
- Dataverse
- Power Pages
- Copilot Studio

#### When to Apply

- Users or application identities receive access errors
- Features, connectors, or actions are unavailable
- DLP, licensing, or environment policies block execution

#### Recommended Actions

- Verify the effective user, service principal, or connection identity
- Grant least-privilege roles, table permissions, web roles, and connection access
- Confirm licenses, capacity, environment settings, and connector eligibility
- Review DLP and authentication policies before changing the solution

#### Why It Helps

- Resolves configuration failures without weakening security
- Separates authorization, licensing, and policy causes

#### Related Causes

- C05 — Incorrect Tool or Component Used for the Workload
- C17 — Identity, Access, Licensing, or Policy Misconfiguration

---

### RP19 — Prepare and Validate Desktop Runtime Readiness

#### Applies To

- Power Automate for desktop
- Attended automation
- Unattended automation
- RPA machines

#### When to Apply

- A desktop flow cannot start, connect, or create a session
- Machine, user session, agent, or Remote Desktop prerequisites are inconsistent

#### Recommended Actions

- Verify machine registration, online status, agent health, and supported versions
- Confirm attended sessions are unlocked or unattended sessions are permitted
- Validate credentials, Remote Desktop permissions, local policies, and connectivity
- Re-register cloned or materially changed machines and test the run context

#### Why It Helps

- Removes environmental causes before debugging flow logic
- Makes authoring and runtime conditions predictable

#### Related Causes

- C18 — Desktop Runtime or Machine Readiness

---

### RP20 — Build Resilient RPA Selectors and Runtime Checks

#### Applies To

- Power Automate for desktop
- UI automation
- Desktop application integrations

#### When to Apply

- UI elements are not found
- Automation fails after application, window, resolution, or timing changes

#### Recommended Actions

- Prefer stable selector attributes and hierarchical anchors
- Wait for windows and elements instead of relying on fixed delays alone
- Validate application state, resolution, DPI, and required controls before actions
- Add recovery paths and test selectors across supported runtime variants

#### Why It Helps

- Reduces failures caused by timing and presentation changes
- Detects environmental drift before destructive actions

#### Related Causes

- C19 — Fragile RPA Selector or Runtime Assumptions

---

### RP21 — Ground Agent Responses and Harden Action Contracts

#### Applies To

- Copilot Studio
- Agents
- Knowledge sources
- Agent actions and plugins

#### When to Apply

- Responses are inaccurate, incomplete, or unsupported
- Agent actions fail or return inconsistent results

#### Recommended Actions

- Use approved, current knowledge sources with explicit grounding boundaries
- Define action schemas, required inputs, permissions, timeouts, and failure responses
- Test representative prompts and action paths, including refusal and escalation cases
- Review analytics and logs, then refine instructions and tool contracts

#### Why It Helps

- Improves answer relevance and trustworthiness
- Makes action failures diagnosable and safe to recover from

#### Related Causes

- C17 — Identity, Access, Licensing, or Policy Misconfiguration
- C20 — Inadequate Agent Grounding or Action Contracts

---

### RP22 — Repair ALM Dependencies and Deployment Configuration

#### Applies To

- Dataverse solutions
- Power Platform Pipelines
- Environment variables
- Connection references

#### When to Apply

- Solution imports or pipeline deployments fail
- Components, dependencies, references, or target settings are missing

#### Recommended Actions

- Read the complete import log and identify missing or versioned dependencies
- Include prerequisites and deploy in a dependency-aware order
- Configure connection references, environment variables, identities, and target policies
- Re-export from a known-good version and isolate unsupported components for manual handling

#### Why It Helps

- Produces repeatable deployments across environments
- Prevents runtime failures caused by incomplete configuration

#### Related Causes

- C17 — Identity, Access, Licensing, or Policy Misconfiguration
- C21 — ALM Dependency or Deployment Configuration Failure

---

### Common Remediation Combinations

#### Reduce Data Volume + Push Processing to the Data Source

Recommended for:

- Delegation issues
- Large dataset issues

#### Defer Non-Essential Processing + Control Execution Frequency

Recommended for:

- Startup slowness
- Navigation slowness

#### Limit Data Payload + Optimize UI Rendering

Recommended for:

- Slow screen rendering

#### Replace Non-Scalable Patterns + Restructure Solution Architecture

Recommended for:

- Systemic performance issues

#### Handle Throttling and Transient Failures + Validate Inputs and Handle Failures Defensively

Recommended for:

- Connector failures, HTTP 429 responses, and unreliable integrations

#### Design Efficient Dataflow ETL + Validate at Production Scale

Recommended for:

- High-volume dataflows and refreshes approaching production workloads

#### Prepare and Validate Desktop Runtime Readiness + Build Resilient RPA Selectors and Runtime Checks

Recommended for:

- Desktop flows that fail because of machine state, timing, or UI drift

#### Ground Agent Responses and Harden Action Contracts + Correct Identity, Access, Licensing, and Policy Configuration

Recommended for:

- Poor agent responses and failed Copilot Studio actions

#### Repair ALM Dependencies and Deployment Configuration + Correct Identity, Access, Licensing, and Policy Configuration

Recommended for:

- Solution import and pipeline deployment failures

## Change Log

### Version 2.0.0

Expanded from a performance-only catalog into a broader Power Platform corrective-action catalog. Added RP13-RP22 and repaired heading/metadata issues.
