# Microsoft 365 Employee Onboarding Automation

A Microsoft 365 employee onboarding workflow built with SharePoint Online, Power Automate, and Microsoft Approvals.

The solution automates employee onboarding approval requests, captures approval decisions, and maintains structured audit information directly in SharePoint.

## Overview

This project demonstrates an end-to-end Microsoft 365 business process automation solution.

A SharePoint Online list acts as the primary data store for employee onboarding requests. When a new request is created, Power Automate automatically initiates an approval workflow.

The approver can approve or reject the request through Microsoft Approvals. The workflow then updates the corresponding SharePoint record with the approval status and audit metadata.

## Technologies

- Microsoft 365
- SharePoint Online
- Power Automate
- Microsoft Approvals
- Microsoft Entra ID
- Microsoft 365 mobile approval experience

## Architecture

The solution follows this workflow:

SharePoint Online  
↓  
Employee Lifecycle Request Created  
↓  
Power Automate Trigger  
↓  
Microsoft Approvals  
↓  
Approval Decision  
↓  
Condition  
↙              ↘  
Approved     Rejected  
↓              ↓  
Update SharePoint Record  
↓  
Store Audit Metadata

## SharePoint Data Model

The `Employee Lifecycle Requests` list stores onboarding information including:

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

Approval-related fields are controlled by the automation rather than the standard user request form.

## Power Automate Workflow

The automated workflow performs the following operations:

1. Detects a new SharePoint onboarding request.
2. Retrieves the employee onboarding information.
3. Creates an approval request using Microsoft Approvals.
4. Waits for the approver's decision.
5. Evaluates the approval outcome.
6. Executes the appropriate Approved or Rejected branch.
7. Updates the original SharePoint record.
8. Records approval audit information.

## Approval Audit Trail

The workflow automatically maintains:

- Approval Status
- Approver Identity
- Approval Date
- Approval Comments

This provides a structured audit trail for each onboarding request.

## Testing

The solution was validated through multiple end-to-end tests.

### Approved Scenario

Verified:

- SharePoint trigger execution
- Approval request generation
- Approval processing
- Status update to `Approved`
- Approver identity capture
- Approval date capture
- Approval comments capture

### Rejected Scenario

Verified:

- SharePoint trigger execution
- Rejection processing
- Status update to `Rejected`
- Approver identity capture
- Approval date capture
- Rejection comments capture

### Additional Validation

The following were also tested:

- Required SharePoint fields remain intact after workflow updates
- Person or Group field mapping for the approver
- Conditional workflow branches
- Power Automate run history
- Mobile approval processing
- Workflow-controlled audit fields
- SharePoint column display-name changes

## Documentation

Detailed technical documentation is available in the `docs` directory:

- [Solution Architecture](docs/architecture.md)
- [SharePoint Data Model](docs/sharepoint-schema.md)
- [Power Automate Workflow](docs/workflow.md)
- [Testing and Validation](docs/testing.md)

## Project Structure

    m365-employee-onboarding-automation/
    │
    ├── README.md
    │
    └── docs/
        ├── architecture.md
        ├── sharepoint-schema.md
        ├── workflow.md
        └── testing.md

## Key Features

- Automated employee onboarding workflow
- SharePoint-based request management
- Microsoft Approvals integration
- Approve and Reject workflow branches
- Automated SharePoint record updates
- Approver identity tracking
- Approval date tracking
- Approval comments capture
- Structured audit trail
- Mobile approval support
- End-to-end workflow validation

## Security and Design Considerations

Workflow-managed approval fields are separated from user-entered onboarding information.

Approval metadata is hidden from the standard SharePoint request form to reduce the risk of manual modification.

The solution uses Microsoft 365 identity and permission controls rather than storing credentials or sensitive authentication information in the repository.

No production credentials, tenant secrets, access tokens, or confidential employee information are included in this repository.

## Future Enhancements

Potential future development includes:

- Power Apps onboarding interface
- Role-based request views
- Multi-stage approvals
- Automated IT provisioning tasks
- Equipment assignment workflows
- Microsoft Teams notifications
- Onboarding completion tracking
- Reporting and dashboard integration
- Employee offboarding automation

## Project Status

**Status:** Completed and Validated

The core SharePoint and Power Automate employee onboarding approval workflow has been successfully implemented and tested.

## Author

**Sam Etemad**

IT Infrastructure & Cloud Security Specialist
