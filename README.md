# Microsoft 365 Employee Onboarding Automation

An end-to-end employee onboarding approval solution built with Microsoft 365, SharePoint Online, Power Automate, and Microsoft Approvals.

## Overview

This project automates employee onboarding requests from submission through approval, decision processing, status updates, and audit tracking.

The solution uses SharePoint Online as the request data layer and Power Automate as the workflow engine.

## Architecture

SharePoint Online  
↓  
When an item is created  
↓  
Power Automate  
↓  
Microsoft Approvals  
↓  
Condition  
↙          ↘  
Approved   Rejected  
↓             ↓  
SharePoint Update  
↓  
Audit Trail

## Technologies

- Microsoft 365
- SharePoint Online
- Power Automate
- Microsoft Approvals
- Microsoft Lists

## SharePoint Data Model

The Employee Lifecycle Requests list includes:

- Title
- Request Type
- Employee Name
- Department
- Job Title
- Manager
- Start Date
- Employment Type
- Location
- Equipment Required
- Status
- Approver
- Approval Date
- Approval Comments

## Workflow

1. A new onboarding request is created in SharePoint.
2. Power Automate triggers automatically.
3. An approval request is sent to the assigned approver.
4. The approver selects Approve or Reject.
5. Power Automate evaluates the approval outcome.
6. The SharePoint item is updated automatically.
7. Approval metadata is stored for audit purposes.

## Approval Audit Trail

The workflow records:

- Approval status
- Approver identity
- Approval date
- Approval comments

## Validation

Both workflow paths were tested successfully:

### Approved Path

- Status updated to Approved
- Approver captured
- Approval date recorded
- Approval comments supported

### Rejected Path

- Status updated to Rejected
- Approver captured
- Approval date recorded
- Rejection comments recorded

## Security and Privacy

This public repository contains sanitized documentation only.

Tenant-specific URLs, organizational data, production exports, user information, credentials, and internal configuration details are intentionally excluded.

## Current Status

Core onboarding approval workflow: Completed and tested.

## Next Phase

Planned enhancements include:

- Power Apps front end
- Request dashboard
- Employee lifecycle tracking
- Offboarding workflow
- Equipment provisioning workflow
- Additional reporting and automation

## Author

Sam Etemad
