# 🏠 How to run locally?
1. Create an Azure App Rego.
2. When creating, no platform is needed to start (add redirect + SPA settings later when turning into a full-stack app)
3. Add permission for API to read user profiles: Azure App Rego > API permissions > Add a permission > MS Graph > 'profile' and 'User.Read'
4. Create a scope: Azure App Rego > Expose an API > Add a scope for admins and users called "API.Access"
5. `cp appsettings.json appsettings.Development.json` (safely gitignored)
6. Populate fields:
   - `{{AUTH_CLIENT_ID}}` Azure App Rego > Overview > copy client ID
   - `{{AUTH_TENANT_ID}}` Azure App Rego > Overview > copy tenant ID
   - `{{AUTH_AUTHORITY}}` Azure App Rego > Overview > Endpoints > copy authority URL (usually the URL with the tenant ID to restrict access for those within the enterprise)
   - `{{AUTH_AUDIENCE}}` app rego > Manage > Expose an API > copy Application ID URI
   - `{{SYSTEM_API_KEY}}` you decide! or just use `openssl rand -base64 32`
7. `dotnet run`

# 🛩️ How to test?
Use the [.http file](./MrJobs.WebApi.http)
1. Login `az login --tenant <AzAppRego tenant ID> --scope <"API.Access" scope>`
2. Obtain a JWT `az account get-access-token --resource <AzAppRego client ID> --scope <"API.Access" scope>`
3. Variables:
   - **@JWT** paste the Azure JWT
   - **@SystemApiKey** paste your custom API key
