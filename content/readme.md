# Notebook Snap Installation Instructions

> Usage of this product confirms your agreement to the following 'Indemnification', and 'Liability disclaimer':

Indemnification: You agree to indemnify, defend and hold harmless BI Tracks, its officers, directors, employees, agents and third parties, for any losses, costs, liabilities and expenses relating to or arising out of your use of or inability to use BI Track's Services, Programs, or any related software services.

See: [Liability disclaimer](liability_disclaimer.md) for details

## System Requirements (all 64-bit):
- Windows 10 or Windows Server 2016 (or later)
- SQL Server 2019 (or later) Express, Standard, or Enterprise Edition
- PowerShell Core 7.1.2 (or later)
- Azure Data Studio
- Python 3.8 (or later)

**Important**: Verify "PowerShell Requirements" using notebook: [Local System Configuration](system_configuration.ipynb)

## Installation Steps:

**Step 1** - Clone from GitHub (using Azure Data Studio)

See: [Cloning with Azure Data Studio](clone_instructions.md)

**Step 2** - Open Install Instructions in ADS.

From ADS, click on the notebook icon:

![](notebook.PNG)

Open the Installation notebook under "Notebook Snap Install"

![](installation.PNG)

**Step 3** - Install the following extension:
- eltsnap

See: [Installing ADS Extensions](install_extensions.md) for step-by-step instructions.

> To Import .**Bacpac** files with Azure Data Studio you will need to install the extension: **SQL Server Dacpac** (Ctrl+Shift+X) 

**Step 4** - Import the following two .Bacpac (data-tier application) files to a SQL Server Instance:
- eltsnap_v2
- elt_framework

![](import_bacpac.PNG)

**Step 5** - **Clone** and *Configure* the **eltSnap Runtime** GitHub Repository: [eltSnap Runtime](https://github.com/Jim-BITracks/eltsnap_runtime)

**Step 6** - (Optional) Customize Runtime Log Directory

This database entry allows you choose an alternate location to store your "Runtime Log files". This option will _unclutter_ your eltSnap Runtime folder.

- Run the following statement in your newly imported **eltsnap_v2** database:

~~~ SQL
INSERT [elt].[application_config] VALUES ('log dir', 'C:\snap\runtime_log');  -- <-- place desired Log Directory here
~~~

**Step 7** - Test the eltSnap runtime by pasting the following command into the Terminal Window (you may need to update the **-server** parameter "localhost" below to specify your SQL Server instance name):

``` powershell
eltsnap_runtime_v2 -server "localhost" -database "eltsnap_v2" -project "Database Log Clean-up"
```

**Step 8** - (Optional) Store runtime license in database

If you have an eltSnap Runtime License, you can place the license in the eltsnap_v2 database (instead of the standard config file). This allows you to update the eltSnap Runtime (e.g., via GitHub 'sync') without needing to then re-apply your Runtime license

- Run the following statements in your **eltsnap_v2** database:

~~~ SQL
DECLARE @servername NVARCHAR(128) = 'SRV1' --<-- place server name here
DECLARE @license NVARCHAR(64) = 'xxxx-xxxx-xxxx-xxx-xxxx-x' --<-- place license number here

DELETE [elt].[application_config] WHERE [setting] = 'runtime license (' + @servername + ')';
INSERT [elt].[application_config] VALUES ('runtime license (' + @servername + ')', @license);
~~~

**Step 9** - (Optional) Sample eltSnap projects are available in GitHub Repository: [Notebook Snap Basics](https://github.com/Jim-BITracks/notebook_snap_basics)