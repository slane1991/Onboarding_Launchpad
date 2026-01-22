🚀 **Automated Deployment of Onboarding Launchpads**

Using Dynatrace Workflows + GitHub‑Hosted Launchpad Templates
This repository contains all files and automation templates required to deploy the Dynatrace Onboarding Launchpad series into any customer tenant. Deployment is fully automated through Dynatrace Workflows, which pull the Launchpad JSON files directly from GitHub.

📘 **Overview**

The Onboarding Launchpad series helps guide new users through Dynatrace with role‑based, customizable content.
This repository enables:

Automated creation of all Launchpads in a target tenant
Automatic mapping of dependencies between Launchpads
One‑time workflow execution (safe to delete afterward)
GitHub‑hosted JSON as the source of truth

You may choose automated deployment (recommended) or manual JSON upload.

⚠️ **Before You Begin**

Automated deployment requires the ability to:

Pull Launchpad JSON files from GitHub
Generate a bearer token via a Dynatrace OAuth client

This means you must:

Temporarily whitelist a few external host patterns
Temporarily store OAuth credentials within the Workflow


Note:

These credentials are used only during deployment.
The Workflow can be deleted immediately after use.
Whitelisted URLs can also be removed afterward.


Manual upload is supported, but you must manually re‑map the Launchpad navigation buttons.


🧩 **Deployment Steps**

1. Create an OAuth Client
Dynatrace’s Documents API requires a bearer token that is generated via OAuth.
Follow Dynatrace's OAuth setup guide:
🔗 https://docs.dynatrace.com/docs/shortlink/oauth


**Steps**

Go to Account Management
Navigate to Identity & access management → OAuth clients
Select Create client
Enter an owner email
Add a description
Assign permissions:

Document Service → Create and edit documents

documents:documents:write

Select Create client
Copy the generated values — you will not be able to view the client secret again


**2. Upload the Workflow Template**
   
Download the prebuilt automation workflow from this repository:
Onboarding Workflow Automation/onboarding-automation-workflow.workflow-template.yaml

Upload in Dynatrace

Go to Workflows
Select Upload
Choose the workflow file
Select Create workflow


Do not run the workflow yet.
Credentials and whitelisting must be configured first.


**3. Insert OAuth Credentials into the Workflow**

Locate the workflow step named:
fetch_bearer_token

Replace these values with your OAuth client details:

client_id
client_secret
resource

Notes

Tokens are valid for 30 seconds
Workflow execution is required only once
The workflow can be removed after successful Launchpad deployment


**4. Whitelist Required External URLs**

Dynatrace must allow outbound access to GitHub and Dynatrace SSO endpoints.
Add each host under:
Settings → General → External requests → + New host pattern
Whitelist the following:
sso.dynatrace.com
raw.githubusercontent.com
api.github.com

Each host must be added separately.

**5. Run the Workflow**

Once credentials and whitelisting are completed:

Select Run workflow
Wait until execution completes
Return to the Dynatrace homepage
Select Browse all
Confirm that all Onboarding Launchpads (prefix “Onboarding - ”) now appear

After verification
You may now:

✔ Delete the workflow
✔ Remove the whitelisted hosts
✔ Configure user access to each Launchpad

By default, Launchpads are not globally shared, allowing customers to control access.
