# Notebook Snap Installation Instructions

> Usage of this product confirms your agreement to the following 'Indemnification', and 'Liability disclaimer':

Indemnification: You agree to indemnify, defend and hold harmless BI Tracks, its officers, directors, employees, agents and third parties, for any losses, costs, liabilities and expenses relating to or arising out of your use of or inability to use BI Track's Services, Programs, or any related software services.

See: [Liability disclaimer](liability_disclaimer.md) for details

## System Requirements:
- Windows 10 or Windows Server 2016 (or later)
- SQL Server 2019 (or later) Express, Standard, or Enterprise Edition
- PowerShell Core 7.0 (or later)
- Azure Data Studio
- Python 3.9 (or later recommended)

**Important**: Verify "PowerShell Requirements" using notebook: [Local System Configuration](system_configuration.ipynb)

## Installation Steps:

> To Deploy a .**dacpac** file with Azure Data Studio you will need to install the extension: **SQL Server Dacpac** (Ctrl+Shift+X) 

**Step 1** - Deploy the following two .dacpac (data-tier application) files to a SQL Server Instance:
- eltsnap_v2
- elt_framework

See: [Deploying a .dacpac File](dacpac_deploy.md) for step-by-step instructions to deploy a .dacpac file to SQL Server

**Step 2** - Reset tables in the **eltsnap_v2** database by running the following stored procedure (using a connection to **eltsnap_v2**):

Use Notebook: [Reset All eltsnap_v2 Tables](reset_all_eltsnap_v2_tables.ipynb)

**Step 3** - Reset tables in the **elt_framework** database by running the following stored procedure (using a connection to **elt_framework**):

Use Notebook: [Reset All eltsnap_v2 Tables](reset_all_elt_framework_tables.ipynb)

**Step 4** - **Clone** and Configure the **eltSnap Runtime** GitHub Repository: [Runtime](https://github.com/Jim-BITracks/eltsnap_runtime)

**Step 5** - Test the eltSnap runtime by pasting the following command into the Terminal Window (be sure to update the **-server** parameter "localhost" below to specify your SQL Server instance name):

``` powershell
eltsnap_runtime_v2 -server "localhost" -database "eltsnap_v2" -project "Log Clean-up"
```

**Step 6** - **Clone** and Configure the **Notebook Snap Basic** GitHub Repository: [Runtime](https://github.com/Jim-BITracks/notebook_snap_basics)