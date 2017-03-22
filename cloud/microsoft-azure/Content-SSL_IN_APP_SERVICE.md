# SSL In App Service (with App Service Certificate)
**NOTE: Existing App Service Certificates should be by default auto renewal. This guide will only discuss about creating new cert.**

## Purchase App Service Certificate
 1. Login to Azure Portal;
 2. Search for "**App Service Certificate**" in the main search box;
 3. Click on **Add** button to create a new cert;
 4. Please submit the following details in the *Certificate* pane.    
    **Name**: Friendly name describing the use of the new cert.    
    **Naked Domain Host Name**: Domain name of the website that you want to apply this cert for. It can be particular subdomain also.    
    **Subscription**: Choose the correct Azure Subscription.    
    **Resource Group**: Choose the correct Resource Group.    
    **Certificate SKU**: Choose "Standard" for single domain or subdomain; Choose "Wild Card" for wildcard cert.    
    **Legal Terms**: Please click and read then click "OK" to agree the terms. Don't skip it!
 5. The deployments of new App Service Certificate will take about 10 minutes. After it is done, please click on **Refresh** to see it appear in the list of App Service Certificates.
 
## Setup App Service Certificate Step 1: Deploying Azure Key Vault
 1. Click on the new App Service Certificate;
 2. There will be an Alert Bar saying "**Configured required Key Vault store ->**". Click on it;
 3. Click on **Step 1: Store** in the **Certificate Status** pane;
 4. Click on **Key Vault Repository: Configure required settings** in the **Key Vault Status** pane;
 5. Click on **Create a new vault** and submit the following information.    
    **Name**: Friendly name describing the use of the Key Vault.    
    **Naked Domain Host Name**: Domain name of the website that you want to apply this cert for. It can be particular subdomain also.    
    **Subscription**: Choose the correct Azure Subscription.    
    **Resource Group**: Choose the correct Resource Group.    
    **Pricing Tier**: Choose "Standard" if **Hsm Backed Keys** feature is not needed; Otherwise, choose "Premium".    
    **Access Policies**: Manage the correct access policies.     
    **Advanced Access Policies**: Leave it as default.
 6. Deployment and saving of Azure Key Vault will take about 1 minute to complete.
 
## Setup App Service Certificate Step 2: Verifying Domain Ownership
 1. The same Alert Bar in previous step now is changed to saying "**Perform required domain verification ->**". Click on it;
 2. Click on **Step 2: Verify** in the **Certificate Status** pane;
 3. For the **Select the method to verify domain ownership** dropdown, change to use **Mail Verification**;
    - The **Domain Verification** does not always work.
 4. Check for the email sent to the stated **Domain Verification Emails** inboxes;
 5. There should be an email with the subject "**Domain Access Verification**" received. If not, click the **Resend Email** button on the **Domain Verification** pane;
 6. The email will be sent by Azure SSL partner, i.e. **GoDaddy**. Click on the verification link to proceed to confirm the ownership of the domain;
 7. Click the **Refresh** button on the **Domain Verification** pane;
 8. Click the **Refresh** button on the **App Service Certificate** pane until there is a notification box at the bottom of it saying "**Certification**";
 9. Make sure all the three checkboxes in Certificate Status pane are ticked.
 
## Import Certificate to App Service
 1. Visit the app service that the certificate needs to be assigned to in the **App Services**;
 2. Go to **SSL certificates** in the **Settings**;
 3. Click **Import App Service Certificate** button;
 4. Choose the new App Service Certificate;
 5. It will take less than 30 seconds to import the App Service Certificate;
 6. Under **SSL bindings**, click on "**Add binding" button;
 7. If the app service has both www and non-www versions, please bind the SSL to both of them.
 8. Done.
 
## What Is The Use Of Azure Key Vault Here?
Azure Key Vault allows us to safeguard our App Service Certificates. App Service Apps will securely load certificates from specified Azure Key Vault for normal operations as well as handle renew, reissue and rekey operations on your App Service Certificates.

## References
 - [Purchase an App Service Certificate](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Purchase-an-App-Service-Certificate)
