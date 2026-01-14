Performance-Report-Generator

This project is provided as-is for internal tooling and automation workflows.

Recommended Environment

PowerShell 7+

Azure Automation (ideal)

Also works locally if variables are injected manually


This PowerShell script generates a formatted OKR performance report for a specified OBoard user and interval.
It can either:

Output HTML locally, or send the report via Microsoft Graph (client-credential flow)

✨ What It Does

Connects to OBoard API using an API token

Looks up a user by email

Fetches that user’s OKRs + Key Results for a selected interval

Builds a hierarchical tree (Objectives → Key Results)

Optionally fetches latest comments (Objectives only)

Renders everything to an email-safe HTML table

Optionally sends the report via Microsoft Graph / SendMail

Key Features

✔ No secrets stored in code (everything pulled from Azure Automation Variables)
✔ Clean HTML layout that works in Outlook / Gmail / webmail
✔ Supports deep links to OBoard UI if configured
✔ Root-only comment fetching avoids noisy KR comments
✔ Configurable description truncation
✔ Fully compatible with Azure Automation Runbooks

Required Azure Automation Variables

Create variables with these exact names:
| Variable Name             | Purpose                                      |
|---------------------------|----------------------------------------------|
| `API-Token`               | OBoard API access token                      |
| `baseurl`                 | Base API endpoint for OBoard                 |
| `UiBase`                  | (Optional) Base URL for UI deep links        |
| `ApplicationClientID`     | Graph app registration (`client_id`)         |
| `ApplicationTenantID`     | Tenant ID for Graph auth                     |
| `ApplicationClientSecret` | Graph client secret                          |
| `SenderEmail`             | UPN/mailbox used for Graph SendMail          |


Notes	No secrets stored in code, only in variables

Ideal for automated OKR reporting in enterprise environments

Output report from the azure runbook :
<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/054b2b0e-c994-4d1d-9584-c8d900b12823" />


Note: Email clients (e.g. Microsoft Outlook, Gmail) may render HTML and CSS differently. As a result, the layout, spacing, or styling of the report may vary depending on the viewer’s application and version.
