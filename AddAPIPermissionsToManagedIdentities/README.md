# Managed Identity API Permission Assigner

Assign Microsoft Graph API permissions to Azure Managed Identities via PowerShell when GUI options aren't available.

## 🚀 Use Cases
- Grant permissions like `SecurityEvents.Read.All` to Logic Apps Managed Identities
- Automate permission assignments in CI/CD pipelines
- Work around GUI limitations in Microsoft Entra ID

## ⚙️ Prerequisites
1. **Azure PowerShell Module**:
   ```powershell
   Install-Module -Name AzureAD -Force -AllowClobber
Required Permissions:

- Global Administrator or Privileged Role Administrator
- Owner role on the target Managed Identity

📋 How to Use
Configure the script:

powershell
Copy
# Replace these values
- $appId = "your-managed-identity-app-id"       # Found in Entra ID → App Registrations
- $objectId = "your-managed-identity-object-id" # Found in Entra ID → Enterprise Applications
- $permission = "SecurityEvents.Read.All"       # Required Graph API permission
Run the script:

```powershell
Copy
.\Assign-ManagedIdentityPermission.ps1
```
Verify:
Check assignments in Entra ID under:

Copy
Enterprise Applications → [Your Managed Identity] → Permissions
🛠️ Script Parameters
Variable	Description	Where to Find
- $appId	Application (Client) ID	Entra ID → App Registrations → Overview
- $objectId	Object ID (Service Principal)	Entra ID → Enterprise Applications → Properties
- $permission	API Permission name (e.g., User.ReadWrite.All)	Microsoft Graph Permissions Reference


🚨 Troubleshooting
- Missing Authorization	Run Connect-AzureAD as Global Admin
- App Role not found	Verify permission exists in Graph permissions list
- 403 Forbidden	Ensure you have Owner rights on the Managed Identity
