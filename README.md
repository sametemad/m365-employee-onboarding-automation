# Microsoft 365 Employee Onboarding Automation

A Microsoft 365 employee onboarding workflow built with **SharePoint Online, Power Automate, and Microsoft Approvals**.

This project demonstrates how an employee onboarding request can be submitted through SharePoint, routed automatically for approval, and updated with approval status and audit information.

---

## Project Overview

Manual employee onboarding processes often involve emails, spreadsheets, follow-ups, and disconnected approval records.

This solution centralizes the onboarding request and approval process using Microsoft 365.

The workflow provides:

- Centralized employee onboarding requests
- Structured SharePoint data
- Automated approval routing
- Approve / Reject workflow logic
- Automatic status updates
- Approver tracking
- Approval date tracking
- Approval comments
- End-to-end workflow validation

---

## Technology Stack

- Microsoft 365
- SharePoint Online
- Power Automate
- Microsoft Approvals
- Microsoft Entra ID
- Microsoft Teams / Outlook approval notifications

---

## Solution Architecture

The workflow follows this architecture:

```text
Employee Onboarding Request
          │
          ▼
   SharePoint Online
          │
          ▼
     Power Automate
          │
          ▼
   Microsoft Approvals
          │
      ┌───┴───┐
      │       │
   Approve   Reject
      │       │
      └───┬───┘
          ▼
 Update SharePoint Record
          │
          ▼
 Status + Approver + Date + Comments
```

### Architecture Diagram

![Microsoft 365 Employee Onboarding Architecture](assets/architecture.png)

---

## Workflow

### 1. Employee Onboarding Request

A new onboarding request is created in the SharePoint **Employee Lifecycle Requests** list.

The request captures structured information required for the onboarding process.

Example fields include:

- Employee Name
- Department
- Job Title
- Manager
- Start Date
- Employment Type
- Location
- Equipment Required
- Request Status
- Approver
- Approval Date
- Approval Comments

![Employee Onboarding Request](assets/approval-request.png)

---

### 2. Power Automate Trigger

The automated cloud flow begins when a new item is created in the SharePoint list.

Trigger:

```text
When an item is created
```

The flow retrieves the onboarding request information and prepares the approval request.

---

### 3. Microsoft Approval

Power Automate creates an approval using:

```text
Start and wait for an approval
```

The designated approver receives the request through the Microsoft 365 approval experience.

The approver can select:

```text
Approve
```

or:

```text
Reject
```

and optionally provide comments.

---

### 4. Conditional Workflow Logic

After receiving the approval response, Power Automate evaluates the outcome.

```text
Approval Outcome
       │
       ▼
    Condition
     /     \
    /       \
Approve     Reject
  │           │
  ▼           ▼
Update       Update
Status       Status
```

The appropriate workflow branch executes automatically.

### Workflow Overview

![Power Automate Workflow Overview](assets/workflow-overview.png)

---

### 5. SharePoint Record Update

Following the approval decision, Power Automate updates the original SharePoint item.

The workflow automatically records:

- Approval Status
- Approver
- Approval Date
- Approval Comments

This creates a centralized audit record for each onboarding request.

### Approval Results

![SharePoint Approval Results](assets/sharepoint-approval-results.png)

---

## SharePoint Data Model

The SharePoint list acts as the primary data source for the workflow.

| Column | Type | Purpose |
|---|---|---|
| Title | Single line of text | Request identifier |
| Request Type | Choice | Type of employee lifecycle request |
| Employee Name | Single line of text | Employee being onboarded |
| Department | Choice / Text | Employee department |
| Job Title | Single line of text | Employee position |
| Manager | Person / Group | Employee manager |
| Start Date | Date | Employment start date |
| Employment Type | Choice | Full-time, part-time, contract, etc. |
| Location | Choice / Text | Work location |
| Equipment Required | Multiple lines / Choice | Required IT equipment |
| Status | Choice | Current workflow status |
| Approver | Person or Group | Approval responder |
| Approval Date | Date and Time | Approval decision timestamp |
| Approval Comments | Multiple lines of text | Approval audit comments |

The **Approver** field uses the SharePoint **Person or Group** data type so the approval responder identity can be mapped directly from Power Automate.

---

## Power Automate Workflow

The workflow contains the following primary stages:

```text
1. SharePoint
   When an item is created

2. Microsoft Approvals
   Start and wait for an approval

3. Condition
   Evaluate approval outcome

4. Approved Branch
   Update SharePoint item
   Status = Approved

5. Rejected Branch
   Update SharePoint item
   Status = Rejected

6. Audit Information
   Store approver
   Store approval date
   Store approval comments
```

---

## Approval Logic

Conceptually, the workflow follows this logic:

```text
IF Approval Outcome = Approve

    Status = Approved
    Approver = Approval Responder
    Approval Date = Current Approval Time
    Approval Comments = Approval Response

ELSE

    Status = Rejected
    Approver = Approval Responder
    Approval Date = Current Approval Time
    Approval Comments = Approval Response
```

This removes the need to manually update the SharePoint request after an approval decision.

---

## Testing and Validation

The solution was tested using multiple employee onboarding requests.

Validation included:

- SharePoint item creation
- Automatic Power Automate trigger execution
- Approval request generation
- Approval notification delivery
- Approve scenario
- Reject scenario
- Approval responder mapping
- SharePoint status updates
- Approval date capture
- Approval comments capture
- Flow run-history verification
- End-to-end workflow validation

Both **Approved** and **Rejected** workflow paths were successfully tested.

---

## Security and Privacy

The public repository uses sanitized demonstration data.

Production organization names, internal identifiers, credentials, employee information, tenant information, and other sensitive data are intentionally excluded from the repository.

The screenshots included in this repository are intended only to demonstrate the technical implementation and workflow design.

---

## Business Value

This solution demonstrates how Microsoft 365 can be used to replace a manual onboarding approval process with a structured automated workflow.

Key benefits include:

- Reduced manual follow-up
- Consistent onboarding requests
- Centralized approval records
- Improved process visibility
- Faster approval handling
- Better auditability
- Standardized employee lifecycle processes
- Extensible architecture for future automation

---

## Future Enhancements

The solution can be extended with:

- Automated Microsoft Entra ID account provisioning
- Microsoft 365 license assignment
- Security group assignment
- Microsoft Teams membership
- SharePoint permission provisioning
- Equipment assignment workflow
- IT service desk integration
- Manager notifications
- HR notifications
- Automated offboarding workflow
- Power Apps front-end
- Power BI reporting dashboard

These enhancements could expand the project from an approval workflow into a broader **Microsoft 365 Employee Lifecycle Automation** solution.

---

## Project Structure

```text
m365-employee-onboarding-automation/
│
├── README.md
│
├── assets/
│   ├── architecture.png
│   ├── workflow-overview.png
│   ├── approval-request.png
│   └── sharepoint-approval-results.png
│
└── docs/
    ├── architecture.md
    ├── sharepoint-schema.md
    ├── workflow.md
    └── testing.md
```

---

## Documentation

Additional technical documentation is available in the `docs` directory:

- [Solution Architecture](docs/architecture.md)
- [SharePoint Data Model](docs/sharepoint-schema.md)
- [Power Automate Workflow](docs/workflow.md)
- [Testing and Validation](docs/testing.md)

---

## Skills Demonstrated

**Microsoft 365 Administration**

SharePoint Online · Microsoft Entra ID · Microsoft 365 Services

**Automation**

Power Automate · Microsoft Approvals · Workflow Design · Conditional Logic

**SharePoint**

List Architecture · Data Types · Person or Group Fields · Workflow Integration

**IT Process Automation**

Employee Onboarding · Approval Workflows · Audit Tracking · Process Standardization

**Security & Administration**

Identity-Aware Workflows · Access Control Concepts · Data Privacy · Administrative Automation

---

## Author

**Sam Etemad**  
**IT Infrastructure & Cloud Security Specialist**

Microsoft 365 · Azure · Fortinet/FortiGate · Networking · Security · IT Automation

🌐 [sametemad.com](https://sametemad.com)  
💻 [GitHub — sametemad](https://github.com/sametemad)

---

## Disclaimer

This repository is a portfolio and technical demonstration project.

All screenshots and examples use sanitized or demonstration data. No confidential organizational information, production credentials, or personally identifiable employee information is intentionally included.

---

© 2026 Sam Etemad
