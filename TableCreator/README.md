# Table Schema Cloner for Microsoft Sentinel

## 📄 Overview

This script allows you to **clone the schema** of an existing Microsoft Sentinel (Log Analytics) table and create a **new table** with the same schema. It supports creating **Analytics**, **Basic**, and **Auxiliary** table types and handles conversion of unsupported dynamic fields in Auxiliary tables.

## 📌 Features

- 🔁 **Schema cloning** from any existing table  
- ⚙️ **Supports Analytics, Basic, and Auxiliary** table creation  
- 📦 **Automatic type conversion** for dynamic fields in Auxiliary tables (via `-ConvertToString`)  
- 🧠 **Manual overrides** for known schema issues (e.g., `SecurityEvent`, `SigninLogs`)  
- ✅ **Validation and defaults** for retention settings  
- 🛠️ Uses **`Invoke-AzRestMethod`** with latest API versions  

## ⚙️ Prerequisites

1. **Azure PowerShell Module**:
   ```powershell
   Install-Module -Name Az -Force -AllowClobber

Log in to Azure:

```Connect-AzAccount```

Required Permissions:

```Microsoft Sentinel Contributor on the workspace```

```Reader at the subscription level```

Update the following in the script:

   ```powershell
$resourceId = "/subscriptions/<your-subscription-id>/resourceGroups/<your-resource-group>/providers/Microsoft.OperationalInsights/workspaces/<your-workspace-name>"
```

## 🚀 How to Use

Copy the PS into Azure CLI, it will then ask to fill up arguments;

   ```powershell
Parameter	Description
-tableName	Name of the existing table to clone schema from
-newTableName	Name of the new table (include _CL suffix)
-type	    Table type: analytics, basic, or auxiliary
-retention	Retention in days (only applies to Analytics tables)
-totalRetention	Total retention in days (applies to all types if supported)
-ConvertToString	Optional. Converts dynamic fields to string for Auxiliary tables
```

## 🛑 Known Limitations
Auxiliary tables do not support dynamic types unless converted using -ConvertToString

Schema fetching relies on getschema operator, which may misreport some field types (e.g., guid fields)

You must manually update the $resourceId before running

##❓ Troubleshooting

Error Message	Suggestion

   ```powershell
403 Forbidden	Verify Microsoft Sentinel Contributor access to workspace
404 Not Found	Check workspace or table name for typos
409 Conflict	Table already exists – the script will update schema if possible
[SKIPPING ... dynamic type ...]	Use -ConvertToString to convert dynamic fields for Auxiliary tables
```
