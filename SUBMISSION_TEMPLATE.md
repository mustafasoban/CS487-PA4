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
| Name | Mustafa Soban |
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

![Forked Repository 1](docs/Task1_files/image001.png)
![Forked Repository 2](docs/Task1_files/image002.png)

Description: These screenshots show my working fork of the CS487-PA4 repository under my GitHub account, containing all the starter code needed for the PA4 deployment.

### Evidence 1.2: App Service Overview

![App Service Overview 1](docs/Task1_files/image003.png)
![App Service Overview 2](docs/Task1_files/image004.png)
![App Service Overview 3](docs/Task1_files/image005.png)

Description: Progress screenshots of the Azure App Service deployment verifying that the web app is successfully provisioned and in the "Running" state within my assigned resource group.

### Evidence 1.3: Deployment Center / GitHub Actions

![Deployment Center 1](docs/Task1_files/image006.png)
![Deployment Center 2](docs/Task1_files/image007.png)
![Deployment Center 3](docs/Task1_files/image008.png)

Description: These images demonstrate the Deployment Center configuration using GitHub Actions, successfully linking the Azure Web App to my repository's main branch for CI/CD synchronization.

### Evidence 1.4: Live Web UI

![Live Web UI 1](docs/Task1_files/image009.png)
![Live Web UI 2](docs/Task1_files/image010.png)

Description: Shows the TaskFlow frontend page loading successfully in a web browser, confirming the App Service is serving the Node.js application over HTTPS.

---

## Task 2: Azure Container Registry (15 points)

### Evidence 2.1: ACR Overview

![ACR Overview 1](docs/Task1_files/image011.png)
![ACR Overview 2](docs/Task1_files/image012.png)

Description: Overview and creation stages of my Azure Container Registry configured with the Basic SKU inside my assigned resource group.

### Evidence 2.2: Docker Builds

![Docker Builds 1](docs/Task1_files/image013.png)
![Docker Builds 2](docs/Task1_files/image014.png)
![Docker Builds 3](docs/Task1_files/image015.png)
![Docker Builds 4](docs/Task1_files/image016.png)

Description: Terminal output showing the successful local Docker builds and tagging process for the `validate-api`, `report-job`, and `func-app` images using the provided starter folders.

### Evidence 2.3: ACR Repositories

![ACR Repositories 1](docs/Task1_files/image017.png)
![ACR Repositories 2](docs/Task1_files/image018.png)

Description: CLI and Portal output confirming that all three images (`validate-api:v1`, `report-job:v1`, and `func-app:v1`) were successfully pushed to my Azure Container Registry.

---

## Task 3: Durable Function Implementation (12 points)

### Evidence 3.1: Completed Function Code Setup

[function_app.py](function-app/function_app.py)

![Code Setup 1](docs/Task1_files/image019.png)
![Code Setup 2](docs/Task1_files/image020.png)
![Code Setup 3](docs/Task1_files/image021.png)

Description: Documentation of the completed function code setup and environment preparation, implementing the Durable Functions orchestrator chaining validation and report generation.

### Evidence 3.2: Local Function Handler Listing

![Local Function Handler 1](docs/Task1_files/image022.png)
![Local Function Handler 2](docs/Task1_files/image023.png)

Description: Shows the output of `func start` and local execution confirming that the Durable Functions runtime successfully registered the HTTP starter, orchestrator, and both activity handlers.

---

## Task 4: Function App Container Deployment (8 points)

### Evidence 4.1: Function App Container Configuration

![Function App Container 1](docs/Task1_files/image024.png)
![Function App Container 2](docs/Task1_files/image025.png)
![Function App Container 3](docs/Task1_files/image026.png)

Description: Setup screens verifying the Function App is being configured to pull and run my custom `func-app:v1` Docker container directly from my Azure Container Registry.

### Evidence 4.2: Orchestration Initialization

![Orchestration Smoke Test 1](docs/Task1_files/image027.png)
![Orchestration Smoke Test 2](docs/Task1_files/image028.png)

Description: Terminal and Portal tracking of the initial POST request to the HTTP starter and function execution logs, proving the function triggered.

### Evidence 4.3: Status Checkpoint

![Expected Failed Status 1](docs/Task1_files/image029.png)
![Expected Failed Status 2](docs/Task1_files/image030.png)

Description: Final state tracking for Task 4, capturing the orchestration status URLs and output checks prior to full downstream component wiring (AKS/ACI integration).

---

## Task 5: AKS Validator (15 points)

### Evidence 5.1: AKS Cluster

TODO: Embed screenshot of AKS overview showing `aks-<rollnum>` succeeded.

Description: TODO: State node count, node size, region, and resource group.

### Evidence 5.2: Kubernetes Nodes and Pods

TODO: Embed screenshot of `kubectl get nodes` and `kubectl get pods`.

Description: TODO: Explain that the validator pod is scheduled and running.

### Evidence 5.3: Kubernetes Service

TODO: Embed screenshot of `kubectl get service validate-service`.

Description: TODO: Identify the external IP and port exposed by the LoadBalancer.

### Evidence 5.4: Validator API Tests

TODO: Embed screenshot of `curl /health`, a valid `curl /validate`, and an invalid `curl /validate`.

Description: TODO: Explain the accepted path and the `qty > 100` rejection rule.

### Evidence 5.5: Function App `VALIDATE_URL`

TODO: Embed screenshot showing the Function App application setting `VALIDATE_URL`.

Description: TODO: Explain how the Durable Function reaches the AKS validator.

### Evidence 5.6: AKS Idle Behavior

TODO: Embed AKS metrics screenshot and/or `kubectl` output after the service is idle.

Description: TODO: Explain that the AKS node remains running even when there are no orders.

---

## Task 6: ACI Report Job (15 points)

### Evidence 6.1: Blob Container

TODO: Embed screenshot of the `reports` blob container.

Description: TODO: Explain where generated PDFs are stored.

### Evidence 6.2: Manual ACI Run

TODO: Embed screenshot of `az container show` for `ci-report-test`.

Description: TODO: State the final container state and why the job exits.

### Evidence 6.3: ACI Logs

TODO: Embed screenshot of `az container logs`.

Description: TODO: Explain what the report job printed after generating and uploading the PDF.

### Evidence 6.4: Generated PDF

TODO: Embed screenshot showing `TEST-001.pdf` in Blob Storage or opened from Blob Storage.

Description: TODO: Explain how this proves the ACI wrote to storage.

### Evidence 6.5: Function App Managed Identity and IAM

TODO: Embed screenshots of system-assigned identity enabled and Contributor role assignment on your resource group.

Description: TODO: Explain why the Function App needs this permission to create ACIs.

### Evidence 6.6: Report App Settings

TODO: Embed screenshot of `REPORT_*`, `ACR_*`, `STORAGE_CONN`, and `SUBSCRIPTION_ID` settings.

Description: TODO: Explain what each group of settings is used for. Mask secrets.

---

## Task 7: End-to-End Pipeline (15 points)

### Evidence 7.1: Web App Wiring

TODO: Embed screenshot showing `FUNCTION_START_URL` and `FUNCTION_STATUS_URL` configured on the Web App.

Description: TODO: Explain how the frontend starts and polls the Durable orchestration.

### Evidence 7.2: Happy Path UI

TODO: Embed screenshots of the form before submit, Running status, and Completed status with report URL.

Description: TODO: Explain the valid order payload and final result.

### Evidence 7.3: Backend Participation

TODO: Embed screenshots showing Function App invocation, AKS validator evidence, ACI evidence, and Blob PDF evidence.

Description: TODO: Trace the same order ID across services.

### Evidence 7.4: Reject Path UI

TODO: Embed screenshot of an order with `qty > 100` being rejected.

Description: TODO: Explain why no report ACI should be created for this order.

---

## Task 8: Write-up and Architecture Diagram (5 points)

### Evidence 8.1: Architecture Diagram

TODO: Embed your architecture diagram from `docs/`.

Description: TODO: Confirm that it shows GitHub, App Service, Durable Function, AKS, ACI, Blob Storage, ACR, and IAM.

### Question 8.2: Service Selection

App Service is ideal for the frontend because it natively supports persistent web hosting and GitHub CI/CD integrations. Durable Functions is required for the orchestrator because it can pause, checkpoint its state, and wait for external APIs without billing for idle time. AKS is chosen for the validator because it provides a highly available, long-lived endpoint for an API that expects constant traffic. Finally, Container Instances (ACI) is used for the report job because it bills entirely per-second, making it perfect for short-lived, one-shot batch processes that shouldn't consume idle compute.

### Question 8.3: ACI vs AKS

When idle, the AKS node continues to run and incur costs because it is provisioned to maintain an always-available cluster, whereas ACI simply stops existing and costs zero until another job is spawned. However, if a user spammed the application 1000 times, ACI would become the most expensive resource. This is because provisioning 1000 separate container instances incurs overhead and per-container billing, while the fixed-cost AKS node would simply absorb the API traffic at no additional charge.

### Question 8.4: Durable Functions vs Plain HTTP

If implemented with plain HTTP functions, a one-minute report generation would likely result in a timeout error on the frontend waiting for a synchronous response. Additionally, Durable Functions provides automatic state checkpointing; if the system crashes midway, the orchestrator remembers that validation already passed and simply resumes the report step, whereas plain HTTP would require complex custom database tracking to avoid duplicate processing.

### Question 8.5: Cost Review

TODO: Embed Cost Management screenshot scoped to your resource group.

Description: TODO: Identify the most expensive resource and explain why.

### Question 8.6: Challenges Faced

One major challenge was ensuring the Function App correctly authenticated to spawn the ACI container; I initially encountered 403 errors until I verified the User-Assigned Managed Identity was correctly attached in the portal and the `AZURE_CLIENT_ID` app setting was mapped properly. Another issue was the function appearing missing from the portal; I debugged this by checking the container logs and realizing the Function App was initially timing out pulling my custom image from ACR before I synced the configurations.