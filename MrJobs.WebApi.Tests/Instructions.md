# 🏠 How to run locally?

1. The integration tests require [appsettings.Tests.json](../MrJobs.WebApi/appsettings.Tests.json)
2. Create using `cp appsettings.Tests.Example.json appsettings.Tests.json` (safely gitignored)
3. Populate with all the same auth settings from [appsettings.json](../MrJobs.WebApi/appsettings.json) + an additional Client Secret.

### Why is the additional Client Secret needed?

Because we can't test Managed Identity outside of Azure or test interactive user flow w/o a user, so we will fallback to testing a Service Principal. This is called 'Client Credentials flow' where our Service Principal will be the Azure App Rego itself and the password is the Client Secret.

### How do I setup Azure App Rego to authenticate against itself?
1. Click on Expose an API > Add a client application
2. Paste the Azure App Rego's client ID and assign to the "API.Access" scope
3. 🏁 Now the Service Principal has permission to call the API
4. Click on API permissions > Add a permission > My APIs
5. Choose the same Azure App Rego
6. Assign it to an app role (the same role as the web job is fine)
7. 🏁 Now the Service Principal has the same RBAC claims as the web job
8. Click on Certificates & secrets
9. Create a new client secret and copy it into appsettings.Tests.json
10. 🏁 This is the "password" the Service Principal
