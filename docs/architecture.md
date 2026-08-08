# Solution Architecture

## Overview

The Microsoft 365 Employee Onboarding Automation solution provides an automated approval workflow for employee onboarding requests.

The architecture combines SharePoint Online, Power Automate, and Microsoft Approvals to provide request management, approval processing, and audit tracking.

## Architecture Flow

Employee Onboarding Request  
↓  
SharePoint Online  
`Employee Lifecycle Requests`  
↓  
Power Automate Trigger  
`When an item is created`  
↓  
Microsoft Approvals  
`Start and wait for an approval`  
↓  
Approval Decision  
↙              ↘  
Approved       Rejected  
↓                 ↓  
Update SharePoint Item  
↓  
Record Approval Metadata

## Components

### SharePoint Online

Acts as the primary data layer for onboarding requests.

It stores employee information, request metadata, equipment requirements, workflow status, and approval audit information.

### Power Automate

Acts as the workflow and orchestration layer.

Responsibilities include:

- Detecting new onboarding requests
- Creating approval requests
- Waiting for approval decisions
- Evaluating approval outcomes
- Updating SharePoint records
- Recording approval metadata

### Microsoft Approvals

Provides the approval interface used by the designated approver.

The approval process supports:

- Approve
- Reject
- Approval comments
- Approver identity
- Response timestamp

## Decision Logic

The workflow evaluates the response returned by Microsoft Approvals.

If approved:

`Status → Approved`

If rejected:

`Status → Rejected`

The workflow then writes the approval metadata back to SharePoint.

## Audit Data

The following information is retained in SharePoint:

- Workflow status
- Approver
- Approval date
- Approval comments

This provides a persistent audit trail for each onboarding request.

## Security Design

The public GitHub repository contains architecture and implementation documentation only.

The following information is excluded:

- Microsoft 365 tenant identifiers
- SharePoint tenant URLs
- Corporate email addresses
- Authentication information
- Connection references
- Internal employee information
- Production workflow exports

## Future Architecture

The solution is designed to support a Power Apps presentation layer.

Future architecture:

Power Apps  
↓  
SharePoint Online  
↓  
Power Automate  
↓  
Microsoft Approvals  
↓  
SharePoint Audit Trail

This will provide a structured user interface while retaining the existing Microsoft 365 automation backend.
