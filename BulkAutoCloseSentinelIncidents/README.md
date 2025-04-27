# Microsoft Sentinel Bulk Incident Closer

![Azure Sentinel Logo](https://azure.microsoft.com/svghandler/sentinel/?width=300&height=300)

A PowerShell script to automatically close all open Microsoft Sentinel incidents in bulk, with configurable batch processing and automatic retries.

## Features

- 🚀 **Bulk closure** of all open incidents regardless of severity
- ⏱️ **Pagination handling** for reliable processing of large volumes
- 🔄 **Automatic retries** for failed operations
- 📊 **Detailed reporting** with success/failure counts
- ⚙️ **Configurable parameters** for batch size and delays

## Prerequisites

- Azure PowerShell module (`Install-Module -Name Az`)
- Required permissions:
  - Microsoft Sentinel Contributor role
  - Log Analytics Contributor role

## Installation


1. Authenticate to Azure:
```powershell
Connect-AzAccount
```

## Configuration
Edit the configuration section in the script:
```
$config = @{
    ResourceGroupName = "YourResourceGroup"
    WorkspaceName    = "YourLAWorkspace"
    SubscriptionId   = "your-subscription-id"
    PageSize         = 100            # Incidents per API call
    RetryAttempts    = 2              # Retries per incident
    DelayBetweenCalls = 2             # Seconds between API calls
}
```

## Usage
Run the script:
   ```powershell
.\Close-SentinelIncidents.ps1
```

## Sample output:
```
Starting bulk incident closure process...
Configuration:
- Page Size: 100
- Retry Attempts: 2
- Delay Between Calls: 2s

Closed incident: 1234-abcd...
Processed 100 incidents | Total closed: 100
...
============================================
Bulk closure process completed
Total incidents closed: 1250
Failed to close: 3
============================================
```
## Troubleshooting

Common Issues:

-Permission errors: Ensure you have Microsoft Sentinel Contributor role

-Throttling: Reduce PageSize or increase DelayBetweenCalls

-Stubborn incidents: Try running the script multiple times


# Script can also be initiated directly from Azure CLI :)
