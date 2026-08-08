# SharePoint Data Model

## Overview

The solution uses a SharePoint Online list named `Employee Lifecycle Requests` as the primary data store for employee onboarding requests.

The list stores employee information, onboarding requirements, workflow state, and approval audit metadata.

## List Schema

| Column | Type | Purpose |
|---|---|---|
| Title | Single line of text | Request title / reference |
| Request Type | Choice | Defines the lifecycle request type |
| Employee Name | Single line of text | Employee full name |
| Department | Choice | Employee department |
| Job Title | Single line of text | Employee job title |
| Manager | Person or Group | Assigned manager |
| Start Date | Date and Time | Employee start date |
| Employment Type | Choice | Employment classification |
| Location | Choice | Employee work location |
| Equipment Required | Choice | Required onboarding equipment |
| Status | Choice | Workflow status |
| Approver | Person or Group | User who completed the approval |
| Approval Date | Date and Time | Approval response timestamp |
| Approval Comments | Multiple lines of text | Approver comments |

## Workflow States

The primary workflow states are:

- Pending
- Approved
- Rejected

A newly submitted request begins in the `Pending` state.

Power Automate changes the status after the approval decision.

## Approval Metadata

After an approval response is received, Power Automate writes audit information back to the corresponding SharePoint item.

### Approver

Stores the identity of the user who responded to the approval request.

### Approval Date

Stores the approval response timestamp.

### Approval Comments

Stores comments submitted during the approval or rejection process.

## Data Flow

Request Created  
↓  
SharePoint Item Created  
↓  
Status = Pending  
↓  
Power Automate Triggered  
↓  
Approval Decision  
↓  
SharePoint Item Updated  
↓  
Status + Approver + Approval Date + Comments

## Design Considerations

Choice columns are used for controlled values such as department, employment type, location, equipment requirements, and workflow status.

Person or Group fields are used where Microsoft 365 identity resolution is required.

Approval metadata is stored directly with the original request to maintain a centralized lifecycle and audit record.

## Privacy

This documentation represents the logical schema of the solution.

Production records, employee information, tenant identifiers, corporate addresses, and other organization-specific information are not included in this public repository.
