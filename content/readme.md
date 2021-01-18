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

## Installation Steps:
**Step 1** - Deploy the following two .dacpac (data-tier application) files to a SQL Server Instance:
- eltsnap_v2
- elt_framework

See: [Deploying a .dacpac File](dacpac_deploy.md) for step-by-step instructions to deploy a .dacpac file to SQL Server

**Step 2** - Reset tables in the **eltsnap_v2** database by running the following stored procedure (using a connection to **eltsnap_v2**):

``` sql
EXEC [dbo].[Reset All Tables] 'Yes';
```

**Step 3** - Reset tables in the **elt_framework** database by running the following stored procedure (using a connection to **elt_framework**):

``` sql
EXEC [dbo].[Reset All Tables];
```