# Dynatrace Onboarding Launchpads

## Description

This project provides a set of **role‑based Dynatrace Onboarding Launchpads** (for example SREs, Dynatrace Admins, Developers) which can be deployed automatically into a Dynatrace tenant.

Launchpads are deployed using **Dynatrace Workflows** and **GitHub‑hosted JSON templates**, enabling consistent onboarding across environments. After deployment, Launchpads can be **fully customised within the Dynatrace UI** to align with customer‑specific tools, processes, and maturity levels.


## What This Provides

- Automated deployment of multiple onboarding Launchpads  
- GitHub‑hosted Launchpad definitions as the deployment source  
- One‑time workflow execution (safe to remove after use)  
- Optional adoption dashboard to track Launchpad usage  
- Full post‑deployment customisation via the Dynatrace UI
  

## Prerequisites

To use the automated deployment, you must be able to:

- Upload and run Dynatrace Workflows  
- Allow outbound access from Dynatrace to GitHub  

No OAuth client, credentials, or authentication setup is required.


## Deployment Steps

### 1. Whitelist Required External URLs

Dynatrace must be allowed to retrieve Launchpad templates from GitHub.

Add the following host patterns under:

**Settings → General → External requests → + New host pattern**

``
raw.githubusercontent.com
``

``
api.github.com
``

Each host must be added separately.


### 2. Deploy the Workflow

[Download the workflow template](https://github.com/slane1991/Onboarding_Launchpad/blob/main/Onboarding%20Workflow%20Automation/onboarding-launchpad-deployment-automation.workflow-template.yaml) from this repository and upload it to Dynatrace:

1. Go to **Workflows**
2. Select **Upload**
3. Choose the workflow JSON file
4. Select **Create workflow**

NOTE: By Default, The Launchpads are globally shared on the tenant. This is for ease of use purposes. If you want to manually control access then you need to disable the update_dashboards_public & update_launchpads_public steps in the Workflow by clicking the (...) button on each step and selecting "Disable" PRIOR to executing the Workflow.


### 3. Run the Workflow

Once the workflow is uploaded and GitHub access is allowed:

1. Open the workflow
2. Select **Run workflow**
3. Wait for execution to complete


### 4. Verify Deployment

After the workflow completes:

- Navigate to **Browse all**
- Confirm the Onboarding Launchpads (prefixed with `Onboarding -`) are visible
- Open a Launchpad to confirm content loads correctly


### 5. Optional Cleanup

After successful verification, you may:

- Delete the workflow  
- Remove the GitHub host patterns from external request settings   


## Manual Deployment Option

If automated deployment is not suitable, Launchpad JSON files can be uploaded manually via the Dynatrace UI.

When using manual deployment:

- Each Launchpad must be imported individually  
- Launchpad "Let's Go" navigation links must be configured manually for the "Onboarding Home Page - Accelerate Your Dynatrace Journey" Launchpad to point to the respective dedicated Launchpads.

Automated deployment is recommended for consistency and reduced setup effort.
