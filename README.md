# MY TAKE ON AZURE LIGHTHOUSE

Greetings my fellow Technology Advocates and Specialists.

In this Session, I will provide real-time insights on __AZURE LIGHTHOUSE__. As Azure Lighthouse provides multiple features, hence for the purpose of this Blog post, we focus on 1) Onboarding Azure Subscription, and 2) Onboarding Azure Resource Group only.

| __WHAT IS COVERED:-__ |
| --------- | 
| Live Recorded Session. |
| Presentation Displayed During Live Demo. |
| Concepts of Azure Lighthouse. |
| How is/was the Management before Azure Lighthouse. |
| Pricing. |
| Real-time Use Cases. |
| Important Pointers on Azure Lighthouse. |
| Deployment Requirement of Azure Lighthouse Using Portal. |
| Step By Step Process to Implement Azure Lighthouse. |
| Verification - Service Provider View. |
| Quick Test. |
| Option to Automate Deployment of Azure Lighthouse. |
| Challenges Encountered. |


| __LIVE RECORDED SESSION:-__ |
| --------- |
| __LIVE DEMO__ was Recorded as part of my Presentation in __JOURNEY TO THE CLOUD 4.0__ Forum/Platform |
| Duration of My Demo = __31 Mins 02 Secs__ |
| Start and End Time = __01:05:06 to 01:36:08__ |


| [![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/C0s6A758mn0/0.jpg)](https://www.youtube.com/watch?v=C0s6A758mn0) |
| --------- |


| __CONCEPTS OF AZURE LIGHTHOUSE:-__ |
| --------- | 
| Azure Lighthouse Service was created by Microsoft keeping in mind the Cloud Service Providers. |
| Azure Lighthouse allows you to enable cross-tenant management and multi-tenant management. |
| Using Azure Lighthouse, service providers can deliver secure managed services and perform numerous management tasks directly on a customer’s subscription or a resource group. |
| There are 2 Views when we manage Cloud:- 1) Service Provider; and  2) Customer |
| Service Provider are mainly responsible for managing 1) Customer Subscription(s) 2) Resource Group(s) 3) Resource(s) and 4) Azure AD Tenant Management (In Some Cases).|
| Imagine a Scenerio, where a Service Provider has to support Azure Resources spread across, for example, in 10 Subscriptions at a time. All Cloud Engineers who work for the Service Provider will then have to switch between 10 Subscription to support Customer`s Cloud Infrastructure. __AZURE LIGHTHOUSE__ eliminates this __PROBLEM STATEMENT__. |

| __HOW IS/WAS THE MANAGEMENT BEFORE AZURE LIGHTHOUSE:-__ |
| --------- | 
| Service Provider has its own Azure Active Directory (AAD) Tenant. In that Tenant, exists the User Identities which provides support to Customer`s Cloud Infrastructure. | 
| Now, Customer also has its own Azure Active Directory (AAD) Tenant. In that Tenant, there exists one or more Subscription(s) which hosts the Azure Resources.| 
| All required User Identities in Service Provider Tenant are added as __GUEST USERS__ (External Identities: __B2B__) in Customer Tenant. Authentication however is happening over Service Provider AAD Tenant. | 
| Guest Users in Customer AAD Tenant is then managed using AAD Groups. |
| Required Role Based Access Control (RBAC) is assigned to the AAD Groups which are either associated to subscription(s), Resource Group(s) or Resource(s). |
| __CATALOG__ Contains one or more __ACCESS PACKAGES__ which in turn contains one or more __AAD GROUPS__. |
| User Assignments becomes relatively easy with Access Packages as Cloud Administrator then does not have to add Users one by one to one or more AAD Groups. |


| __PRICING:-__ |
| --------- |
| Azure Lighthouse powered by the Azure delegated resource management technology is available at no additional charge. Partners who use these capabilities on Azure services such as Log Analytics, Security Center, etc. will continue to pay for the underlying services. If an underlying service is free (Azure Policy, Azure Resource Health and others), then there are no changes and these services will continue to be free of charge. |
| Refer the Link: [Azure Lighthouse Pricing](https://azure.microsoft.com/en-us/pricing/details/azure-lighthouse/#:~:text=Azure%20Lighthouse%20powered%20by%20the,available%20at%20no%20additional%20charge.) |


| __REAL-TIME USE CASES:-__ |
| --------- |
| Azure Lighthouse are typically used for below Scenarios:- |
| 1.) Customer`s Azure Consumption (Billing). |
| 2.) Managing Customer`s Cloud Infrastructure (Azure Services) over Portal. |
| 3.) Customer`s Azure Tenant Management.  |


| __IMPORTANT POINTERS ON AZURE LIGHTHOUSE:-__ |
| --------- |
| We can only onboard one Subscription at a time. |
| We can onboard one or more Resource Group(s). |
| This deployment must be done by a non-guest account in the customer's tenant who has a role with the Microsoft.Authorization/roleAssignments/write permission, such as Owner, for the subscription being onboarded (or which contains the resource groups that are being onboarded). |


| __DEPLOYMENT REQUIREMENT OF AZURE LIGHTHOUSE USING AZURE PORTAL:-__ |
| --------- |
| In order to Onboard a Subscription or Resource Group, we need 2 Subscriptions. One will Simulate as __SERVICE PROVIDER__ and the other as __CUSTOMER__.  |
| The Non Guest User Account should have __Owner__ RBAC Permission on both Subscriptions.  |
| Refer the Github link for [Azure Lighthouse Samples] (https://github.com/Azure/Azure-Lighthouse-samples) |


| __STEP BY STEP PROCESS TO IMPLEMENT AZURE LIGHTHOUSE:-__ |
| --------- |
| __SERVICE PROVIDER:-__ |
| Create 2 Azure Active Directory Security Groups where exists the Subscription simulating as __Service Provider__:- 1) LH-Contributor, and 2) LH-Reader |
| __LH-Contributor__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ivq3y7ou5rv8whtip6oq.png) |
| __LH-Reader__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/uysghbhqt6o3n1ek8ix7.png) | 
| Add Required User(s) to the respective AAD Groups |
| __CUSTOMER:-__ | 
| Use the __Auto Deploy__ option provided in Github Azure Lighthouse samples:- |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4rh5olatf60i1vmhggum.JPG) |
| Below is how it looks on clicking __Auto Deploy__ option. Details are filled manually. This is executed on Subscription simulated as __CUSTOMER__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3vrstkst3ubxrl7x84g2.jpg) |
| __Explanation on the Details:-__ |
| __Subscription__ = Name of the Subscription in Customer Tenant.|
| __Region__ = location of the Azure Resources deployed in the Customer Tenant Subscription. |
| __MSP Offer Name__ = Custom Name indicating the Name of the Service Provider. |
| __MSP Offer Description__ = Custom Description of the Service Provider.  |
| __Managed by Tenant ID__ = Tenant ID of the Service Provider |
| __Authorizations__ = This Field has 3 Elements to it - 1) __principalId__ = Object ID of the Security AAD Group Created in Service Provider Tenant, 2) __roleDefinitionId__ = Built-in RBAC IDs (Here in this Example, it is __Contributor__), and 3) __principalIdDisplayName__ = Name of the Security AAD Group Created in Service Provider Tenant  |
| Below is how the __Authorizations__ values are passed as:- |
| [{"principalId": "27c96d91-3162-4ea6-ad36-e05944a4864a", "roleDefinitionId": "b24988ac-6180-42a0-ab88-20f7382dd24c", "principalIdDisplayName": "LH-Contributor"}] |
| __Validation Passed:-__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rr42jalp0vn2ovh9l11h.jpg) |
| __Successful Deployment:-__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/masogwhfm8g5ehgxn69z.jpg) |

| __VERIFICATION - SERVICE PROVIDER VIEW:-__ |
| --------- |
| Customer Subscription is now listed in the Service Provider Subscription Pane. |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9ax6af2eot63urflbeq9.jpg) |
| __My Customers__ View - Customer  |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/be9smj4rb706b7ik248m.jpg) |
| __My Customers__ View - Delegations  |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zpk7yhs2w00dfpkjcr2s.jpg) |

| __QUICK TEST:-__ |
| --------- |
| Deploy a Test __User Assigned Managed Identity__ in Customer Subscription from Service Provider Subscription __without__ switching to Customer Subscription |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rpac3z2hbuq5jikjk0zm.jpg) |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8dc85yr48u2hkcovo51u.jpg) |


| __OPTIONS TO AUTOMATE DEPLOYMENT OF AZURE LIGHTHOUSE:-__ |
| --------- |
| 1.) __Using Powershell and CLI__ |
| https://docs.microsoft.com/en-us/azure/lighthouse/how-to/onboard-customer#create-an-azure-resource-manager-template |
|  2.) __Using Terraform__ |
| __Definition -__ https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/lighthouse_definition |
| __Assignment -__ https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/lighthouse_assignment |


| __CHALLENGES ENCOUNTERED__ |
| --------- |

| __Issues__ | __Descriptions__ |
| --------- | --------- |
| __No Azure DevOps Integration with Azure Lighthouse__ | For Management and support of Azure Services over Portal, Azure Lighthouse fits, to a certain extent but if Customer follows the path of DevOps (IaC and CI/CD), then unfortunately we have to fall back to the approach described in the Section - __How is/was the Management before Azure Lighthouse.__   |
| __Azure Managed Resource Group with Deny Assignment__ | Azure Services like __Azure Databricks__ when deployed also deploys its own Managed Resource Group (Where the resources gets created during the runtime of Databricks Cluster). This Managed Resource Group has an Deny Assignment which is by design of Microsoft. As observed, if such is the case, then Azure Lighthouse cannot onboard those Resource Group(s). |
| __Access to Key Vault Secret protected by Access Policies__ | As explained, the Service Provider Identities __DOES NOT__ reside in the Customer Tenant using Azure Lighthouse. Key Vault Access Policies are Applied either on User Identities (Guest or Non Guest), AAD Groups, Service Principal(s) or Managed Identities to Access Keys, Secrets and Certificates. But As Service Provider Identities does not exists in Customer Tenant, it becomes a challenge and hence unfortunately we have to fall back to the approach described in the Section - __How is/was the Management before Azure Lighthouse.__   |
| __Resources with Granular RBAC__ | In order to explain this topic better, I take the example of __Azure Kubernetes Service (AKS)__. In order for __Kubectl__ to connect to AKS, Correct RBAC assignment is required to User Identities (Guest or Non Guest) or AAD Group(s). The RBAC here I am referring to is __Azure Kubernetes Service Cluster User Role__. The Problem Statement here is Service Provider AAD Group assigned to Built-in RBAC (Contributor or Reader) is used to onboard a Subscription or one/more Resource Group(s). These does not allow Service Provider Identities to connect to AKS using Kubectl. Also, Service Provider Identities does not exists in Customer Tenant to assign those required AKS RBAC, and hence it becomes a challenge. Unfortunately we then have to fall back to the approach described in the Section - __How is/was the Management before Azure Lighthouse.__    |
