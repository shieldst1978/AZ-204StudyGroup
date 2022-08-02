**Session 1**
Deploy VM
new-azresourcegroupdeployment -Name "AZ-204-Study_Group" -TemplateFile  "AZ204Session1VM_Template.json" -TemplateParameterFile "AZ204Session1VM_Parameters.json"
Standard_B1s

**Session 2**
*Deploy Storage Account using Azure CLI:*
    az storage account create --resource-group AZ-204-Study_Group --name az204studygrpstorageacc --location --access-tier cool --allow-blob-public-access true

*Deploy Blob Storage Container using Azure CLI*
    az storage container create --account-name az204studygrpstorageacc --name az204container --public-access blob

*Deploy Storage Queue using Azure CLI*
    az storage queue create --account-name az204studygrpstorageacc --name az204queue

*Deploy Storage Share using Azure CLI*
    az storage share create --account-name az204studygrpstorageacc --name az204share

*Create a Storage Account Policy with a template*
    az storage account management-policy create --account-name az204studygrpstorageacc --policy AZ204Session2BlobLifecyclePolicy.json --resource-group AZ-204-Study_Group

*Upload a file using AZCopy*
    azcopy copy "azcopy.txt" "https://az204studygrpstorageacc.blob.core.windows.net/az204container?sp=racwdli&st=2022-06-24T14:16:45Z&se=2022-06-25T22:16:45Z&spr=https&sv=2021-06-08&sr=c&sig=ttqPM9YYoQZuPqoIAgBoEECvOrB91VSQsqM0H7zHzfI%3D"

**Session 3**
*Download a .net app*
dotnet new webapp -n AZ-204WebApp -f net6.0 && cd AZ-204WebApp

*Deploy WebApp using defaults*
az webapp up --sku S1 --name AZ-204StudyGroupWebApp --resource-group AZ-204-Study_Group --location UKSouth

*Redeploy Web App*
az webapp up

**Session 4**
*Scale App Service Plan back up* 
az appservice plan update --name shields_t_asp_9624 --resource-group AZ-204-Study_Group --sku S1

*Create a deployment slot for staging environment*
az webapp deployment slot create --name AZ-204StudyGroupWebApp --resource-group AZ-204-Study_Group --slot staging

*deploy to staging*
az webapp deployment source