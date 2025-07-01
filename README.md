# Azure Data Factory – AAS Firewall IP Whitelisting Automation

This repository contains an Azure Data Factory (ADF) pipeline that automates the process of whitelisting IP addresses in Azure Analysis Services (AAS) using a secure and parameterized approach.

## Problem Statement

In many enterprise environments, adding IP addresses to AAS firewall settings requires manual updates in the Azure portal and elevated access roles, which is not scalable or secure. This ADF solution helps automate the process securely.

## What This Pipeline Does

- Reads AAS metadata (Subscription ID, Resource Group, Cube Name) from a configuration table in Azure SQL DB
- Fetches existing firewall rules from AAS using the Azure Management REST API
- Merges the new IP range with existing rules
- Updates the firewall rule list via a PATCH request
- Enables the firewall automatically if it's disabled
- Supports parameterized IPs and environment selection

## Pipeline Name

`Cube_FirewallUpdate_Automate`

## Parameters

| Name             | Description                              |
|------------------|------------------------------------------|
| `EnvName`        | Environment tag (e.g., UAT, DEV)         |
| `IpStartRange`   | Start IP address to whitelist            |
| `IpEndRange`     | End IP address to whitelist              |
| `IpFirewallName` | Friendly name for the firewall rule      |

## Security

- Uses ADF Managed Identity (MSI) — no secrets or credentials needed
- Requires RBAC with at least `Microsoft.AnalysisServices/servers/write` permission

## Files

- `Cube_FirewallUpdate_Automate.json` – Exported pipeline definition
- `README.md` – Documentation for setup and usage

## Notes

- `PATCH` is used for updating the firewall settings.
- Existing rules are preserved by merging old and new rules inside the pipeline.
- Do not use duplicate firewall rule names — AAS won’t allow them.

## Future Enhancements

- Delete specific IPs via ADF
- Whitelist multiple IPs in one run
- Add logging or notification integration

---
## For detailed step, 
please see my article - https://www.c-sharpcorner.com/article/automating-azure-analysis-services-aas-firewall-whitelisting-using-azure-data/

## Contributing

Feel free to fork, raise issues (https://github.com/Tharunkumar-hub/ADF-AAS-Firewall-Automation/issues), or submit improvements by raising Pull Request !
