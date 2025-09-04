# Teaching CRON Jobs

## 🌐 MrJobs.WebApi
- A bare-minimum ASP.NET Web API
- Hosted on an Azure Web App, on an Azure App Service Plan
- Has a CI/CD pipeline (auto-triggered GH Action)
- Uses 2 types of auth strategies:
  1. MSAL via Azure App Rego for federated users and Azure Service Principals for Managed Identity
  2. Custom API key for other backends/CRON jobs that need to bypass OAuth

## 🌐🧪 MrJobs.WebApi.Tests
- Integration tests for both auth strategies
- E2E: JWT from Azure and authenticating with an in-memory [MrJobs.WebApi](./MrJobs.WebApi/)
- Azure OAuth is tested using Client Credentials flow (using a Client Secret)

## 🎮 MrJobs.WebJob.DotNet
- A bare-minimum console app
- Obtains a JWT access token from the Azure App Rego via Managed Identity
- Makes a single HTTP request to the Web API authorized using the JWT
- Has CI/CD pipelines (manually-triggered GH Action)
- View Kudu logs after deploying to confirm success

## 🐚 MrJobs.WebJob.PowerShell
- A PowerShell example (alternative Web Job example)
- Makes a single HTTP request to the Web API authorized using the custom API key

## ⚙️ Internal (self-hosted) job
- ❌ An anti-pattern...
- ❌ When devs run locally, these internal jobs will auto-run, possibly mutating shared dev/staging data unintentionally
- ❌ Adds complexity to a dev's mental model of the app
- ✅ Exposing endpoints for CRON job tasks simplifies the backend (it's just another endpoint)
- ✅ Allows operations teams to have control of the job (change the timer/pause/manually trigger) all w/o touching the main backend

## ☁️ IaC
TODO: add Azure bicep instructions
