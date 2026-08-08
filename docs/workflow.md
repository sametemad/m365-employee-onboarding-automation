# Power Automate Workflow

## Overview

The onboarding workflow is triggered automatically when a new employee onboarding request is created in the SharePoint `Employee Lifecycle Requests` list.

## Workflow Logic

1. SharePoint creates a new onboarding request.
2. Power Automate detects the new item using the `When an item is created` trigger.
3. The workflow sends an approval request through Microsoft Approvals.
4. The approver reviews the employee onboarding details.
5. The approval outcome is evaluated using a condition.
6. The SharePoint record is updated automatically.

## Approval Path

If the request is approved:

- Status is updated to `Approved`
- Approver identity is recorded
- Approval date is recorded
- Approval comments are stored when provided

## Rejection Path

If the request is rejected:

- Status is updated to `Rejected`
- Approver identity is recorded
- Approval date is recorded
- Rejection comments are stored

## Audit Fields

The workflow maintains the following audit metadata:

- Status
- Approver
- Approval Date
- Approval Comments

## Workflow Architecture

SharePoint  
↓  
When an item is created  
↓  
Start and wait for an approval  
↓  
Condition  
↙              ↘  
Approved     Rejected  
↓              ↓  
Update SharePoint Item

## Design Notes

The approval and audit fields are hidden from the standard SharePoint request form to prevent users from manually modifying workflow-controlled values.

Power Automate remains responsible for updating these fields after the approval decision.

This design separates user-entered request data from system-managed approval metadata and helps maintain a consistent audit trail.
