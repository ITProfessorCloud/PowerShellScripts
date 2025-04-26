# BulkTurnOnAnalyticRules

# Microsoft Sentinel Analytics Rule Enabler

Automatically enable ALL analytics rules from installed Microsoft Sentinel solutions while preserving MITRE ATT&CK mappings.

## 📌 Features

- **Bulk activation** of all rule templates across all installed solutions
- **MITRE ATT&CK preservation** (Tactics, Techniques, Sub-techniques)
- **Detailed reporting** with CSV export
- **Safe execution** with error handling
- Supports both **enabled** and **disabled** rule states

## ⚙️ Prerequisites

1. **Azure PowerShell Module**:
   ```powershell
   Install-Module -Name Az -Force -AllowClobber

Required Permissions:

- **Microsoft Sentinel Contributor role on the workspace**

- **Reader role on the subscription level**

Environment Info:

- **Subscription ID**

- **Resource Group containing your Log Analytics workspace**

- **Workspace name**

##  🚀 How to Use
Configure the script:
Edit these variables at the top of the script:

```powershell
$subscriptionId = "<your-subscription-id>"
$resourceGroupName = "<your-resource-group>"
$workspaceName = "<your-workspace-name>"
$enableRules = "Yes"  # "Yes" to enable, "No" to create disabled
```

Run the script (you can copy & paste it into Azure CLI)

## ❓ Troubleshooting
```
403 Forbidden	Verify Microsoft Sentinel Contributor role assignment
404 Not Found	Check workspace name spelling
409 Conflict	Rule already exists - safe to ignore
