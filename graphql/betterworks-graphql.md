# BetterWorks GraphQL Schema

## Overview

This conceptual GraphQL schema represents the BetterWorks continuous performance management platform API surface. BetterWorks provides an enterprise platform for OKR-based goal setting, check-ins, feedback, recognition, calibration, and performance ratings. The schema models the core domain objects accessible via the BetterWorks REST API at https://developers.betterworks.com/ and is intended as a reference for understanding the data model and relationships within the platform.

## Schema Source

- **Provider:** BetterWorks
- **API Reference:** https://developers.betterworks.com/documentation/
- **Base URL:** https://app.betterworks.com/services/core
- **Schema Type:** Conceptual GraphQL (derived from REST API documentation)

## Core Domain Areas

### Users and Organization

The platform models users with roles, managers, teams, and departments. Users are the central entity connecting goals, feedback, check-ins, and performance data.

- `User` — core user identity with profile fields
- `UserDetails` — extended user profile including employment metadata
- `UserRole` — role assignments within the platform (admin, manager, employee)
- `Manager` — manager-subordinate relationship
- `Team` — group of users sharing goals or reporting structure
- `TeamDetails` — extended team metadata including hierarchy
- `Department` — organizational unit grouping teams
- `DepartmentDetails` — extended department metadata
- `OrganizationDetails` — top-level org configuration and settings

### OKRs and Goals

OKRs (Objectives and Key Results) are the primary performance construct. The schema captures the full OKR hierarchy from objectives through key results and progress tracking.

- `OKR` — parent container for an objective with its key results
- `OKRDetails` — extended OKR metadata including alignment and period
- `OKRType` — enumeration of OKR types (company, team, individual)
- `Objective` — qualitative goal statement
- `ObjectiveDetails` — extended objective metadata including owner, comments, status
- `KeyResult` — measurable outcome tied to an objective
- `KeyResultDetails` — extended key result metadata with current and target values
- `Progress` — current progress state of a goal or key result
- `ProgressUpdate` — a recorded progress update event

### Alignment

Alignment represents how goals relate to each other across the organization hierarchy.

- `Alignment` — link between two OKRs or objectives
- `AlignmentDetails` — metadata about an alignment relationship
- `AlignmentType` — enumeration of alignment types (parent-child, supporting)
- `AlignmentMetric` — aggregate alignment measurement for analytics

### Check-Ins

Check-ins are structured conversations between managers and employees about goal progress.

- `CheckIn` — a scheduled or ad-hoc check-in event
- `CheckInDetails` — full check-in record including notes, status, participants

### Reviews and Feedback

The platform supports structured performance reviews and continuous feedback.

- `Review` — a performance review instance
- `ReviewDetails` — extended review data including ratings and comments
- `ReviewCycle` — a defined review period (e.g., annual, mid-year)
- `ReviewType` — enumeration of review types (self, peer, manager, 360)
- `FeedbackRequest` — a request for feedback sent to a user
- `FeedbackResponse` — a response to a feedback request

### Recognition

BetterWorks supports peer recognition via praise and badges.

- `Praise` — a recognition message sent from one user to another
- `PraiseDetails` — extended praise record with reactions and visibility
- `Badge` — a named recognition award that can accompany praise

### Periods

Goal periods define the time boundaries for OKRs.

- `GoalPeriod` — the time window for a set of goals
- `Period` — a generic time period reference
- `PeriodDetails` — extended period metadata including start, end, and status

### Integrations

BetterWorks integrates with enterprise systems to sync data and automate workflows.

- `Integration` — a configured integration between BetterWorks and an external system
- `SlackIntegration` — Slack-specific integration configuration
- `JiraIntegration` — Jira-specific integration configuration
- `SalesforceIntegration` — Salesforce-specific integration configuration
- `WorkdayIntegration` — Workday-specific integration configuration for HRIS sync

### Analytics and Reporting

The platform provides analytics on engagement, alignment, and performance.

- `AggregateAnalytics` — rolled-up analytics across the organization
- `EngagementMetric` — measurement of user engagement with the platform
- `PerformanceMetric` — measurement of performance outcomes
- `Report` — a generated report artifact
- `Analytics` — analytics query result container

### API Access and Webhooks

- `APIKey` — an API credential for programmatic access
- `Token` — an OAuth or session token
- `Webhook` — a configured webhook endpoint for event delivery
- `WebhookEvent` — a webhook event payload record

## Types Count

This schema defines **62 named types** covering the full BetterWorks platform surface.

## Usage Notes

- This is a conceptual schema. BetterWorks exposes a REST API; this GraphQL schema is a representational model of that API surface.
- All queries and mutations map to underlying REST endpoints documented at https://developers.betterworks.com/documentation/
- The schema uses standard GraphQL scalar types: `ID`, `String`, `Int`, `Float`, `Boolean`, `DateTime`
- Pagination follows a cursor-based connection pattern
- Authentication uses OAuth 2.0 bearer tokens via the BetterWorks authorization server
