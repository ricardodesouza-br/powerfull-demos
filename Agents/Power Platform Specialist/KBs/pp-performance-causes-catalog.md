---
title: Power Platform Causes Catalog
document_type: CausesCatalog
domain: LowCode
product_family: Microsoft Power Platform

owner: Low Code Team
version: 1.0.0
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
  - troubleshooting
  - diagnostics
  - scalability
  - architecture
  - operations

related_documents:
 - none
---
<!-- markdownlint-disable MD024 MD025 -->

# Power Platform Causes Catalog

## Purpose

This document provides a structured catalog of diagnosable causes across Power Platform solutions, including performance, reliability, security, automation, agent, and application lifecycle management (ALM) concerns.

Each cause includes:

- Category
- Applies To
- Description
- Typical Symptoms
- Validation Signals
- Recommended Actions
- Likelihood
- Impact
- Related Causes
- Reference

Use this catalog to support troubleshooting, root-cause analysis, and traceable remediation planning. Validate a cause using the listed signals before selecting a corrective pattern.

## Causes Catalog

## C01 — Non-Delegable Query on Large Dataset

### Category

Data / Canvas App

### Applies To

- Canvas Apps
- Large datasets
- Data sources used by Canvas Apps

### Description

The app is using non-delegable filtering, sorting, or formula patterns against a large data source, causing client-side processing and incomplete or slow results.

### Typical Symptoms

- Slow gallery loads
- Partial result sets
- Degraded search responsiveness
- Degraded filter responsiveness on large lists or tables

### Validation Signals

- Delegation warnings in formulas
- Issue worsens when data volume grows
- Performance improves when query scope is reduced

### Recommended Actions

- Refactor formulas to delegable patterns
- Reduce data scope
- Use pagination when delegation is not possible
- Use alternative data access strategies where delegation cannot be achieved

### Likelihood

High

### Impact

High

### Related Causes

- C02 — Excessive Data Loading at App Start
- C03 — Large Dataset Without Data Shaping or Pagination
- C07 — Inefficient Query or Filter Design in Flows or Data Access

### Reference

Performance & Scalability → Delegation & Data Shaping

## C02 — Excessive Data Loading at App Start

### Category

Data Loading / Canvas App

### Applies To

- Canvas Apps

### Description

The app loads more data or executes more logic than necessary during initialization, increasing startup time and perceived slowness.

### Typical Symptoms

- Slow app startup
- Delayed first interaction
- Long splash screens
- Long loading states

### Validation Signals

- Large collections loaded in OnStart
- Many connector calls before the first screen is usable
- Better performance when startup logic is disabled or deferred

### Recommended Actions

- Lazy-load data
- Defer non-critical operations
- Fetch only what is required for the initial user task

### Likelihood

High

### Impact

High

### Related Causes

- C01 — Non-Delegable Query on Large Dataset
- C03 — Large Dataset Without Data Shaping or Pagination
- C07 — Inefficient Query or Filter Design in Flows or Data Access

### Reference

Performance & Scalability → Minimize On-Load Work

## C03 — Large Dataset Without Data Shaping or Pagination

### Category

Data / Scalability

### Applies To

- Canvas Apps
- Power Automate
- Large datasets
- Data access patterns

### Description

The solution attempts to process or display too much data at once without narrowing scope, filtering at source, or paginating results.

### Typical Symptoms

- Performance degrades sharply as data grows
- List or grid rendering becomes slow
- Search operations become unstable
- Sort operations become unstable

### Validation Signals

- Queries return broad datasets
- No paging strategy exists
- Issue becomes severe only at higher volumes

### Recommended Actions

- Filter earlier
- Paginate results
- Reduce row retrieval scope
- Shape data before bringing it into the app or flow

### Likelihood

High

### Impact

High

### Related Causes

- C01 — Non-Delegable Query on Large Dataset
- C02 — Excessive Data Loading at App Start
- C07 — Inefficient Query or Filter Design in Flows or Data Access
- C13 — Datastore Choice Not Aligned with Solution Needs

### Reference

Performance & Scalability → Delegation & Data Shaping / Minimize On-Load Work

## C04 — Monolithic App or Flow Design

### Category

Architecture

### Applies To

- Canvas Apps
- Power Automate
- Apps with many screens
- Flows with many responsibilities

### Description

A single app or flow is handling too many unrelated responsibilities, creating maintenance and runtime overhead.

### Typical Symptoms

- Slow overall responsiveness
- Difficult troubleshooting
- Changes in one area affect unrelated operations
- Oversized flows
- Oversized apps

### Validation Signals

- One app contains too many screens, components, or data sources
- One flow performs unrelated tasks end-to-end
- Performance improves when logic is split

### Recommended Actions

- Split large apps into modular apps
- Split large flows into modular flows
- Isolate responsibilities
- Move reusable logic into child flows or reusable components

### Likelihood

Medium

### Impact

High

### Related Causes

- C02 — Excessive Data Loading at App Start
- C05 — Incorrect Tool or Component Used for the Workload
- C06 — Long-Running Synchronous Process Instead of Asynchronous Design
- C11 — Poor Reuse or Component Strategy Leading to Repeated Heavy Logic

### Reference

Architecture & Solution Design Principles / Development Best Practices

## C05 — Incorrect Tool or Component Used for the Workload

### Category

Architecture / Solution Fit

### Applies To

- Canvas Apps
- Power Automate
- Power Platform components
- Workload design decisions

### Description

The solution uses a Power Platform component for a scenario it is not optimized for, such as using a Canvas App as a background processor or a flow for interactive UI behavior.

### Typical Symptoms

- Persistent slowness despite optimization attempts
- Fragile behavior
- Poor scalability for the workload type

### Validation Signals

- Workload pattern does not match the platform component design
- Issue is structural rather than formula-specific

### Recommended Actions

- Reassign workload to the appropriate component pattern
- Redesign for correct platform usage
- Move long-running processes to asynchronous patterns where appropriate

### Likelihood

Medium

### Impact

High

### Related Causes

- C04 — Monolithic App or Flow Design
- C06 — Long-Running Synchronous Process Instead of Asynchronous Design
- C13 — Datastore Choice Not Aligned with Solution Needs

### Reference

Architecture & Solution Design Principles

## C06 — Long-Running Synchronous Process Instead of Asynchronous Design

### Category

Flow / Architecture

### Applies To

- Power Automate
- Long-running processes
- Flow orchestration patterns

### Description

A flow or process keeps a long-running execution path active instead of queueing or decoupling the work asynchronously.

### Typical Symptoms

- Long flow runtimes
- Unstable executions
- Timeouts
- Degraded responsiveness for downstream operations

### Validation Signals

- A single run handles all processing in one execution path
- Heavy sequential actions
- Performance improves when work is split or queued

### Recommended Actions

- Queue work
- Split processing into separate stages
- Use asynchronous orchestration
- Reduce time spent in a single run

### Likelihood

Medium

### Impact

High

### Related Causes

- C04 — Monolithic App or Flow Design
- C05 — Incorrect Tool or Component Used for the Workload
- C09 — Misused Parallelism or Unsafe Concurrency
- C11 — Poor Reuse or Component Strategy Leading to Repeated Heavy Logic

### Reference

Architecture & Solution Design Principles

## C07 — Inefficient Query or Filter Design in Flows or Data Access

### Category

Flow / Data Access

### Applies To

- Power Automate
- Data access logic
- Connector-based retrieval
- Flow queries

### Description

The solution retrieves more records than necessary or performs broad checks rather than targeted queries.

### Typical Symptoms

- Slow flow executions
- Excessive API calls
- Delays before data-dependent steps execute

### Validation Signals

- Broad “list all” patterns
- Post-filtering after data retrieval
- Excessive columns or repeated connector calls
- Run duration and request count increase with unrelated records

### Recommended Actions

- Filter and select columns at the source
- Use targeted queries, indexed fields, and pagination where supported
- Avoid repeated lookups by caching or reusing results within a run
- Measure request volume and execution time before and after the change

### Likelihood

High

### Impact

High

### Related Causes

- C01 — Non-Delegable Query on Large Dataset
- C03 — Large Dataset Without Data Shaping or Pagination
- C08 — Inefficient Power Query or Dataflow Transformations
- C14 — Throttling or Transient Service Limits

### Reference

Performance & Scalability → Delegation, Data Shaping, and Source Filtering

## C08 — Inefficient Power Query or Dataflow Transformations

### Category

Dataflow / ETL

### Applies To

- Dataflows
- Power Query
- ETL into Dataverse
- ETL into Data Warehouses

### Description

Dataflows apply unnecessary transformations or fail to filter early at the source, increasing processing cost and refresh time.

### Typical Symptoms

- Slow refreshes
- Delayed data availability
- ETL bottlenecks affecting downstream app performance

### Validation Signals

- Many transformation steps
- Full refreshes on large datasets
- No source-side data reduction

### Recommended Actions

- Reduce transformation steps
- Filter at the source
- Use incremental refresh where supported

### Likelihood

Medium

### Impact

High

### Related Causes

- C03 — Large Dataset Without Data Shaping or Pagination
- C07 — Inefficient Query or Filter Design in Flows or Data Access
- C12 — Missing or Weak Monitoring for Degraded Performance
- C13 — Datastore Choice Not Aligned with Solution Needs

### Reference

Performance & Scalability → Optimize Power Query and Dataflows

## C09 — Misused Parallelism or Unsafe Concurrency

### Category

Flow / Concurrency

### Applies To

- Power Automate
- Parallel Branches
- Loop Concurrency
- Concurrent Updates

### Description

Parallel branches or loop concurrency are used without considering race conditions, conflicting updates, or workload suitability.

### Typical Symptoms

- Intermittent failures
- Inconsistent processing times
- Data conflicts
- Hard-to-reproduce slowdowns

### Validation Signals

- Concurrency enabled in loops
- Conflicting record updates
- Performance becomes unstable rather than simply slow

### Recommended Actions

- Reassess concurrency settings
- Isolate independent actions
- Serialize conflicting updates
- Apply parallelism only where it safely reduces total runtime

### Likelihood

Low

### Impact

Medium

### Related Causes

- C04 — Monolithic App or Flow Design
- C06 — Long-Running Synchronous Process Instead of Asynchronous Design

### Reference

Performance & Scalability → Use Parallelism Thoughtfully

## C10 — Lack of Scale Testing Before Production

### Category

Validation / Performance Engineering

### Applies To

- Canvas Apps
- Power Automate
- Dataverse
- Power Pages
- Production Readiness Validation

### Description

The solution was not tested with realistic data volumes or user load, causing bottlenecks to appear only in production-like conditions.

### Typical Symptoms

- Solution performs well in development
- Solution slows significantly in production

### Validation Signals

- No documented scale tests
- Problems appear only with production-size datasets
- Problems appear only with production-level concurrency

### Recommended Actions

- Perform scale testing
- Simulate realistic workloads
- Use performance insights to identify bottlenecks

### Likelihood

High

### Impact

Medium

### Related Causes

- C01 — Non-Delegable Query on Large Dataset
- C02 — Excessive Data Loading at App Start
- C03 — Large Dataset Without Data Shaping or Pagination
- C07 — Inefficient Query or Filter Design in Flows or Data Access
- C08 — Inefficient Power Query or Dataflow Transformations
- C13 — Datastore Choice Not Aligned with Solution Needs

### Reference

Performance & Scalability → Testing at Scale

## C11 — Poor Reuse or Component Strategy Leading to Repeated Heavy Logic

### Category

Development / Maintainability

### Applies To

- Canvas Apps
- Power Automate
- Component Libraries
- Child Flows
- Shared Logic

### Description

The solution repeats formulas, UI logic, or flow sequences instead of reusing components or child flows, increasing maintenance complexity and potentially increasing execution overhead.

### Typical Symptoms

- Similar logic repeated across screens
- Similar logic repeated across flows
- Difficult optimization because the same issue exists in multiple places

### Validation Signals

- Duplicate formulas or actions detected
- Multiple similar flows with slight variations
- No reusable component strategy

### Recommended Actions

- Centralize reusable logic into components
- Use child flows
- Adopt reusable templates

### Likelihood

Medium

### Impact

Medium

### Related Causes

- C04 — Monolithic App or Flow Design
- C06 — Long-Running Synchronous Process Instead of Asynchronous Design

### Reference

Development Best Practices → Reuse and Components

## C12 — Missing or Weak Monitoring for Degraded Performance

### Category

Operations / Monitoring

### Applies To

- Canvas Apps
- Power Automate
- Dataverse
- Power Pages
- Environments
- Operational Monitoring

### Description

The environment lacks monitoring, notifications, operational reviews, or analytics, delaying detection and validation of performance issues.

### Typical Symptoms

- Users report performance issues informally
- Regressions are not detected early
- Improvements cannot be objectively measured

### Validation Signals

- No alerts
- No review routines
- No historical metrics
- No use of monitoring capabilities

### Recommended Actions

- Configure notifications
- Use platform analytics
- Use admin center monitoring
- Establish review routines
- Define measurable success criteria

### Likelihood

High

### Impact

Medium

### Related Causes

- C01 — Non-Delegable Query on Large Dataset
- C02 — Excessive Data Loading at App Start
- C03 — Large Dataset Without Data Shaping or Pagination
- C04 — Monolithic App or Flow Design
- C05 — Incorrect Tool or Component Used for the Workload
- C06 — Long-Running Synchronous Process Instead of Asynchronous Design
- C07 — Inefficient Query or Filter Design in Flows or Data Access
- C08 — Inefficient Power Query or Dataflow Transformations
- C09 — Misused Parallelism or Unsafe Concurrency
- C10 — Lack of Scale Testing Before Production
- C11 — Poor Reuse or Component Strategy Leading to Repeated Heavy Logic
- C13 — Datastore Choice Not Aligned with Solution Needs

### Reference

Monitoring & Maintenance → Establish Monitoring / Governance Operations

## C13 — Datastore Choice Not Aligned with Solution Needs

### Category

Architecture / Data Platform

### Applies To

- Dataverse
- SharePoint Lists
- Excel
- Relational Workloads
- Mission-Critical Data

### Description

The solution uses spreadsheets or lists where a more appropriate relational or mission-critical datastore should be used.

### Typical Symptoms

- Performance degradation with relational complexity
- Weak scalability
- Brittle query patterns

### Validation Signals

- Heavy reliance on flat-file storage
- Heavy reliance on list-based storage for relational workloads
- Heavy reliance on list-based storage for high-volume workloads

### Recommended Actions

- Re-evaluate datastore selection
- Move appropriate workloads to Dataverse
- Redesign data access patterns around the selected platform

### Likelihood

Medium

### Impact

High

### Related Causes

- C01 — Non-Delegable Query on Large Dataset
- C03 — Large Dataset Without Data Shaping or Pagination
- C05 — Incorrect Tool or Component Used for the Workload
- C08 — Inefficient Power Query or Dataflow Transformations

### Reference

Architecture & Solution Design Principles → Use the Right Tool for the Job

## C14 — Throttling or Transient Service Limits

### Category

Reliability / Operations

### Applies To

- Power Automate
- Dataverse
- Connectors
- Integrations

### Description

The workload exceeds service protection, connector, or request limits, or encounters temporary downstream failures that are not handled safely.

### Typical Symptoms

- HTTP 429 responses
- Intermittent connector failures
- Retry storms or long delays
- Failures concentrated during bursts or peak load

### Validation Signals

- Run history contains throttling or retry-after details
- Request volume or concurrency rises before failures
- The same operation succeeds after a delay

### Recommended Actions

- Reduce burst traffic and filter earlier
- Use bounded retries that honor retry-after guidance
- Batch or queue work and define a terminal failure path

### Likelihood

Medium

### Impact

High

### Related Causes

- C06 — Long-Running Synchronous Process Instead of Asynchronous Design
- C07 — Inefficient Query or Filter Design in Flows or Data Access
- C09 — Misused Parallelism or Unsafe Concurrency

### Reference

Operations & Reliability → Service Protection and Retry Handling

## C15 — Trigger Scope or Duplicate Processing

### Category

Flow / Event Processing

### Applies To

- Power Automate
- Event-driven integrations
- High-volume workloads

### Description

Triggers are too broad, self-generated updates re-trigger the process, or multiple flows process the same event without idempotency controls.

### Typical Symptoms

- Duplicate records or notifications
- Unexpected run frequency
- Infinite or repeating flow runs
- Conflicting updates

### Validation Signals

- Trigger conditions accept unrelated events
- The flow writes to its own trigger record
- Multiple flows subscribe to the same event
- Parallel runs share the same business record

### Recommended Actions

- Narrow trigger conditions and use event filters
- Add correlation or processed flags and idempotent writes
- Review concurrency and consolidate duplicate subscriptions

### Likelihood

Medium

### Impact

High

### Related Causes

- C09 — Misused Parallelism or Unsafe Concurrency
- C14 — Throttling or Transient Service Limits

### Reference

Reliability & Operations → Trigger Design and Idempotent Processing

## C16 — Missing Validation or Failure Handling

### Category

Reliability / Data Quality

### Applies To

- Power Automate
- Canvas Apps
- Connectors
- Dataverse

### Description

Inputs, null values, connector responses, or failure paths are not validated before the process continues.

### Typical Symptoms

- InvalidTemplate or schema errors
- Unclear partial failures
- Broken downstream actions after one bad record
- No actionable notification or replay path

### Validation Signals

- Required fields are assumed rather than checked
- Errors are swallowed or run-after paths are absent
- Failed inputs cannot be identified or replayed

### Recommended Actions

- Validate schemas and required values before actions
- Add explicit conditions, scopes, run-after paths, and notifications
- Preserve correlation IDs and failed inputs for diagnosis

### Likelihood

High

### Impact

High

### Related Causes

- C07 — Inefficient Query or Filter Design in Flows or Data Access
- C14 — Throttling or Transient Service Limits

### Reference

Reliability & Operations → Defensive Validation and Error Handling

## C17 — Identity, Access, Licensing, or Policy Misconfiguration

### Category

Security / Governance

### Applies To

- Power Apps
- Power Automate
- Dataverse
- Power Pages
- Copilot Studio

### Description

The effective identity lacks permissions, licensing, capacity, connector access, or policy clearance required by the solution.

### Typical Symptoms

- Access denied or missing content
- Triggers or connectors cannot be enabled
- Features are unavailable
- Actions fail only for particular users or environments

### Validation Signals

- Security roles, table permissions, web roles, or connection ownership differ by user
- DLP, authentication, licensing, or environment policies block the operation
- The same operation succeeds with an appropriately privileged test identity

### Recommended Actions

- Verify effective identities and grant least-privilege access
- Check licenses, capacity, connector eligibility, and environment settings
- Review DLP and authentication policies without bypassing governance

### Likelihood

High

### Impact

High

### Related Causes

- C05 — Incorrect Tool or Component Used for the Workload
- C21 — ALM Dependency or Deployment Configuration Failure

### Reference

Security & Governance → Identity, Access, Licensing, and Policy Configuration

## C18 — Desktop Runtime or Machine Readiness

### Category

RPA / Operations

### Applies To

- Power Automate for desktop
- Attended automation
- Unattended automation
- RPA machines

### Description

The desktop runtime, machine registration, user session, agent, permissions, or connectivity does not satisfy the execution mode requirements.

### Typical Symptoms

- Machine not found or offline
- Session cannot be created
- Attended flow is blocked by a locked session
- Unattended flow fails to connect

### Validation Signals

- Machine status, agent service, Remote Desktop permissions, or local policies are invalid
- Runtime and authoring versions differ
- Re-registering or correcting the machine restores execution

### Recommended Actions

- Validate machine health, registration, connectivity, credentials, and supported versions
- Confirm attended sessions are active and unlocked or unattended prerequisites are met
- Re-register machines after cloning or major configuration changes

### Likelihood

Medium

### Impact

High

### Related Causes

- C19 — Fragile RPA Selector or Runtime Assumptions

### Reference

RPA Operations → Machine, Session, and Runtime Readiness

## C19 — Fragile RPA Selector or Runtime Assumptions

### Category

RPA / UI Automation

### Applies To

- Power Automate for desktop
- UI automation
- Desktop applications

### Description

Selectors or action timing depend on unstable UI attributes, fixed delays, or a specific resolution, DPI, window state, or application version.

### Typical Symptoms

- UI element not found
- Automation fails after an application update
- Intermittent failures between authoring and runtime machines

### Validation Signals

- Selector attributes change between runs
- The application or window is not ready when an action runs
- Failures vary by resolution, DPI, session, or application state

### Recommended Actions

- Use stable attributes and hierarchical anchors
- Wait for application state and validate required controls
- Test across supported runtime configurations and add recovery paths

### Likelihood

High

### Impact

High

### Related Causes

- C18 — Desktop Runtime or Machine Readiness

### Reference

RPA Engineering → Resilient Selectors and Runtime Checks

## C20 — Inadequate Agent Grounding or Action Contracts

### Category

Agents / Knowledge and Actions

### Applies To

- Copilot Studio
- Agent knowledge sources
- Agent actions and plugins

### Description

An agent lacks current, authoritative grounding or has ambiguous action inputs, permissions, failure handling, or escalation behavior.

### Typical Symptoms

- Irrelevant, incomplete, or unsupported answers
- Actions fail, time out, or produce inconsistent results
- The agent cannot explain or recover from a tool failure

### Validation Signals

- Expected content is absent, stale, conflicting, or inaccessible
- Action schemas and required permissions are unclear
- Representative prompts and failure paths are not tested

### Recommended Actions

- Use approved knowledge sources and define grounding boundaries
- Specify action schemas, permissions, timeouts, and failure responses
- Test representative prompts, inspect analytics, and refine instructions iteratively

### Likelihood

Medium

### Impact

High

### Related Causes

- C17 — Identity, Access, Licensing, or Policy Misconfiguration

### Reference

Agent Engineering → Grounding, Tool Contracts, and Safe Failure Handling

## C21 — ALM Dependency or Deployment Configuration Failure

### Category

ALM / Deployment

### Applies To

- Dataverse solutions
- Power Platform Pipelines
- Environment variables
- Connection references

### Description

Deployment fails because prerequisites, versions, connection references, environment variables, target policies, or supported components are missing or inconsistent.

### Typical Symptoms

- Solution import errors
- Missing component or dependency messages
- Pipeline deployment succeeds partially or fails in a target environment

### Validation Signals

- Import logs identify missing dependencies or version conflicts
- Target configuration differs from the source environment
- Connections or environment variables are unresolved

### Recommended Actions

- Read the complete import log and deploy dependencies in order
- Configure target connection references, environment variables, identities, and policies
- Re-export a known-good version and isolate unsupported components for manual handling

### Likelihood

Medium

### Impact

High

### Related Causes

- C17 — Identity, Access, Licensing, or Policy Misconfiguration

### Reference

ALM & Deployment → Dependency Management and Environment Configuration

## Change Log

### Version 2.0.0

Broadened the performance causes catalog into a Power Platform causes catalog, completed C07, normalized headings, and added C14-C21.
