<div align="center">

# PA4 Submission: TaskFlow Pipeline

<img alt="GitHub only" src="https://img.shields.io/badge/Submit-GitHub%20URL%20Only-10b981?style=for-the-badge">
<img alt="Total points" src="https://img.shields.io/badge/Total-100%20points-7c3aed?style=for-the-badge">

</div>

<div style="background:#f5f3ff;color:#111827;border-left:6px solid #6330bc;padding:14px 18px;border-radius:10px;margin:18px 0;">
Copy this file to <code style="color:#111827;background:#ddd6fe;padding:2px 4px;border-radius:4px;">SUBMISSION.md</code>. Put every screenshot in <code style="color:#111827;background:#ddd6fe;padding:2px 4px;border-radius:4px;">docs/</code>, embed it under the correct task, and write a short description below each image explaining what it proves. The grader should not need any file outside this repository.
</div>

## Student Information

| Field | Value |
|---|---|
| Name | [YOUR NAME] |
| Roll Number | [YOUR ROLL NUMBER] |
| GitHub Repository URL | [YOUR GITHUB REPO URL] |
| Resource Group | `rg-sp26-[YOUR ROLL NUMBER]` |
| Assigned Region | `uaenorth` [OR] `ukwest` |

## Evidence Rules

- Use relative image paths, for example: `![AKS nodes](docs/aks-nodes.png)`.
- Every image must have a 1-3 sentence description below it.
- Azure Portal screenshots must show the resource name and enough page context to identify the service.
- CLI screenshots must show the command and output.
- Mask secrets such as function keys, ACR passwords, and storage connection strings.


## Task 1: App Service Web App (15 points)

### Evidence 1.1: Forked Repository

![Forked Repository](docs/Task1_files/image012.png)

Description: This screenshot shows my working fork of the CS487-PA4 repository under my GitHub account, containing all the starter code needed for the PA4 deployment.

### Evidence 1.2: App Service Overview

![App Service Overview](docs/Task1_files/image005.png)

Description: Shows the Azure App Service overview page verifying that the web app is in the "Running" state within my assigned resource group and region.

### Evidence 1.3: Deployment Center / GitHub Actions

![Deployment Center](docs/Task1_files/image022.png)

Description: Demonstrates that the Deployment Center is configured with GitHub Actions, successfully linking the Azure Web App to my repository's main branch for CI/CD.

### Evidence 1.4: Live Web UI

![Live Web UI](docs/Task1_files/image008.png)

Description: Shows the TaskFlow frontend page loading successfully in a web browser, confirming the App Service is serving the Node.js application over HTTPS.

---

## Task 2: Azure Container Registry (15 points)

### Evidence 2.1: ACR Overview

![ACR Overview](docs/Task1_files/image015.png)

Description: Overview of my Azure Container Registry configured with the Basic SKU inside my assigned resource group.

### Evidence 2.2: Docker Builds

![Docker Builds](docs/Task1_files/image003.png)

Description: Terminal output showing the successful local Docker builds for the `validate-api`, `report-job`, and `func-app` images using the provided starter folders.

### Evidence 2.3: ACR Repositories

![ACR Repositories](docs/Task1_files/image028.png)

Description: CLI output confirming that all three images (`validate-api:v1`, `report-job:v1`, and `func-app:v1`) were successfully pushed to my Azure Container Registry.

---

## Task 3: Durable Function Implementation (12 points)

### Evidence 3.1: Completed Function Code

[function_app.py](function-app/function_app.py)

Description: The completed function code implements a Durable Functions orchestrator that first yields to the `validate_activity` and, if the order is valid, proceeds to spawn the ACI via the `report_activity`.

### Evidence 3.2: Local Function Handler Listing

![Local Function Handler](docs/Task1_files/image019.png)

Description: Shows the output of `func start` confirming that the Durable Functions runtime successfully registered the HTTP starter, orchestrator, and both activity handlers.

---

## Task 4: Function App Container Deployment (8 points)

### Evidence 4.1: Function App Container Configuration

![Function App Container](docs/Task1_files/image001.png)

Description: Verifies that the Function App is configured to pull and run my custom `func-app:v1` Docker container from my Azure Container Registry.

### Evidence 4.2: Orchestration Smoke Test

![Orchestration Smoke Test](docs/Task1_files/image011.png)

Description: Terminal output of the initial POST request to the HTTP starter, proving the function triggered and returned the standard management URLs (including the instance ID).

### Evidence 4.3: Expected Failed Status Before Downstream Wiring

![Expected Failed Status](docs/Task1_files/image025.png)

Description: Shows the orchestration status as "Failed" because it attempted to reach the AKS validator before the `VALIDATE_URL` environment variable was configured, which is the expected checkpoint behavior here.

---

## Task 5: AKS Validator (15 points)

### Evidence 5.1: AKS Cluster

![AKS Cluster](docs/Task1_files/image007.png)

Description: Portal overview of the AKS cluster showing it successfully provisioned with a single Standard_B2s node in my resource group.

### Evidence 5.2: Kubernetes Nodes and Pods

![K8s Nodes and Pods](docs/Task1_files/image030.png)

Description: CLI output of `kubectl get nodes` and `kubectl get pods`, proving the node is ready and the validator pod is in the Running state.

### Evidence 5.3: Kubernetes Service

![Kubernetes Service](docs/Task1_files/image014.png)

Description: CLI output of `kubectl get service validate-service` displaying the assigned LoadBalancer EXTERNAL-IP and port 8080.

### Evidence 5.4: Validator API Tests

![Validator API Tests](docs/Task1_files/image009.png)

Description: Curl requests showing the `/health` endpoint responding, a valid order returning `valid: true`, and an invalid order (`qty > 100`) returning `valid: false`.

### Evidence 5.5: Function App `VALIDATE_URL`

![VALIDATE_URL Setting](docs/Task1_files/image021.png)

Description: Shows the Function App's configuration blade where `VALIDATE_URL` is set to the AKS LoadBalancer IP, linking the orchestrator to the validator microservice.

### Evidence 5.6: AKS Idle Behavior

![AKS Idle Behavior](docs/Task1_files/image004.png)

Description: Proves that the AKS node and pod remain constantly running and available even when there is no active traffic or orders being processed.

---

## Task 6: ACI Report Job (15 points)

### Evidence 6.1: Blob Container

![Blob Container](docs/Task1_files/image018.png)

Description: Shows the `reports` container successfully created inside the designated Azure Storage Account to hold the generated PDFs.

### Evidence 6.2: Manual ACI Run

![Manual ACI Run](docs/Task1_files/image027.png)

Description: CLI output verifying the manual ACI execution (`ci-report-test`) transitioned to a "Succeeded" state and exited after completing its batch work.

### Evidence 6.3: ACI Logs

![ACI Logs](docs/Task1_files/image010.png)

Description: Container logs displaying the internal script output, confirming the PDF generation and successful upload to blob storage.

### Evidence 6.4: Generated PDF

![Generated PDF](docs/Task1_files/image029.png)

Description: Shows the newly created PDF file existing within the Azure Blob Storage `reports` container.

### Evidence 6.5: Function App Managed Identity and IAM

![Managed Identity](docs/Task1_files/image006.png)

Description: Displays the user-assigned managed identity attached to the Function App, granting it the necessary permissions to dynamically spawn ACI containers without hardcoded credentials.

### Evidence 6.6: Report App Settings

![Report App Settings](docs/Task1_files/image024.png)

Description: Shows the Function App environment variables configured with the ACR details, resource group, and storage connection strings necessary for the ACI creation SDK call.

---

## Task 7: End-to-End Pipeline (15 points)

### Evidence 7.1: Web App Wiring

![Web App Wiring](docs/Task1_files/image002.png)

Description: Verifies that the Web App's configuration includes the `FUNCTION_START_URL` and `FUNCTION_STATUS_URL`, completing the frontend-to-backend connection.

### Evidence 7.2: Happy Path UI

![Happy Path UI](docs/Task1_files/image017.png)

Description: Shows the full Web App lifecycle for a valid order: submitting the form, showing the "Running" state, and eventually reaching "Completed" with a generated report link.

### Evidence 7.3: Backend Participation

![Backend Participation](docs/Task1_files/image013.png)

Description: Shows Azure Monitor/Logs confirming the orchestrator executed, AKS received the validation request, and the ephemeral ACI was spawned to write the PDF for this specific order.

### Evidence 7.4: Reject Path UI

![Reject Path UI](docs/Task1_files/image026.png)

Description: Shows the Web App immediately rejecting an invalid order (`qty > 100`). Because the orchestrator short-circuits here, no ACI report job was spawned, saving compute resources.

---

## Task 8: Write-up and Architecture Diagram (5 points)

### Evidence 8.1: Architecture Diagram

![Architecture Diagram](docs/Task1_files/image020.png)

Description: My system architecture diagram illustrating the CI/CD pipeline, the orchestrator's integrations with AKS and ACI, and the final output flow to Blob Storage.

### Question 8.2: Service Selection

App Service is ideal for the frontend because it natively supports persistent web hosting and GitHub CI/CD integrations. Durable Functions is required for the orchestrator because it can pause, checkpoint its state, and wait for external APIs without billing for idle time. AKS is chosen for the validator because it provides a highly available, long-lived endpoint for an API that expects constant traffic. Finally, Container Instances (ACI) is used for the report job because it bills entirely per-second, making it perfect for short-lived, one-shot batch processes that shouldn't consume idle compute.

### Question 8.3: ACI vs AKS

When idle, the AKS node continues to run and incur costs because it is provisioned to maintain an always-available cluster, whereas ACI simply stops existing and costs zero until another job is spawned. However, if a user spammed the application 1000 times, ACI would become the most expensive resource. This is because provisioning 1000 separate container instances incurs overhead and per-container billing, while the fixed-cost AKS node would simply absorb the API traffic at no additional charge.

### Question 8.4: Durable Functions vs Plain HTTP

If implemented with plain HTTP functions, a one-minute report generation would likely result in a timeout error on the frontend waiting for a synchronous response. Additionally, Durable Functions provides automatic state checkpointing; if the system crashes midway, the orchestrator remembers that validation already passed and simply resumes the report step, whereas plain HTTP would require complex custom database tracking to avoid duplicate processing.

### Question 8.5: Cost Review

![Cost Management](docs/Task1_files/image023.png)

Description: The Azure Cost Analysis dashboard scoped to my resource group. The single most expensive resource was the AKS cluster (specifically the Virtual Machine Scale Set), as it provisions dedicated VM compute that bills constantly for as long as the cluster is active, unlike the serverless consumption resources.

### Question 8.6: Challenges Faced

One major challenge was ensuring the Function App correctly authenticated to spawn the ACI container; I initially encountered 403 errors until I verified the User-Assigned Managed Identity was correctly attached in the portal and the `AZURE_CLIENT_ID` app setting was mapped properly. Another issue was the function appearing missing from the portal; I debugged this by checking the container logs and realizing the Function App was initially timing out pulling my custom image from ACR before I synced the configurations.