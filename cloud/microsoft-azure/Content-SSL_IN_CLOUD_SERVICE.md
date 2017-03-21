# SSL In Cloud Service (with RapidSSL)

 ![RapidSSL](https://getcert.rapidssl.com/rcm/rapidssl/images/logo.gif)

## Purchase SSL on RapidSSL
 1. Login to [RapidSSL](https://www.rapidssl.com/);
 2. Click on "Renew" button if you are renewing the cert;
    - If you are buying a new cert for a new domain, please choose "Buy" button.
 3. An email will be sent to the **Technical Contact Email** that is entered in RapidSSL.
    - The subject of the email will be "**Action required: approve RapidSSL SSL certificate**".
    - The Technical Contact person needs to click on the link in the email to approve the use of SSL/TLS certificate request in the domain.
 4. After the SSL/TLS certificate request is approved, please generate **CSR (Certificate Signing Request)**.
    - Launch **Internet Information Services (IIS) Manager** on local computer;
    - Click on the server name;
    - From the center menu, double click the "**Server Certificates**" button in the IIS section;    
      ![Server Certificates button in IIS Manager](https://www.digicert.com/images/support-images/iis8/iis8-csr-1.png)
    - From the "**Actions**" pane on the right, click on "**Create Certificate Request...**";    
      ![Create Certificate Request...](https://www.digicert.com/images/support-images/iis8/iis8-csr-2.png)
    - In the "**Distinguished Name Properties**" window, submit the information as follows.    
      **Common Name**: The name through which the certificate will be accessed, usually it's the fully-qualified domain name, e.g., www.domain.com or api.domain.com;    
      **Organization**: The legally registered name of our organization/company. This will be displayed to public, please be careful;    
      **Organizational Unit**: The name of our department within the organization, eg. "Software Development Team";    
      **City/Localit**: The city in which our organization is located, eg. "Toa Payoh";    
      **State/Province**: The state in which our organization is located, eg. "Singapore";    
      **Country/Region**: Two-digit country code of the country in which our organization is located, eg. "SG".
    - In the "**Cryptographic Service Provider Properties**" window, submit the following information.    
      **NOTE: RapidSSL requires us to use RSA and a 2048-bit key to generate the CSR.**
      **Cryptographic Service Provider**: In the drop-down list, select "**Microsoft RSA SChannel Cryptographic Provider**".    
      **Bit Length**: Please choose "**2048**".
    - Click the ... box to browse to a location where we want to save the CSR file.
      **NOTE: Remember the filename that is chosen and the location to which it is saved. The file is required later.**    
      ![Saving CSR as text file](https://www.digicert.com/images/support-images/iis8/iis8-csr-5.png)
    - Done, the CSR is now saved in a text file.
 5. Go back to RapidSSL website and submit the CSR text content (Yes, everything in the CSR file);
 6. After the submission is approved, an email with the subject "**Your RapidSSL certificate is ready**";
    - There is instructions in the email guiding us on how to install the certificate on Windows server. The guide is not covering topic about PaaS web hosting on Azure, so we will ignore it.
 7. Click on the link in the email which points to instructions guiding us on how to install the certificate;
 8. We will be brought to the RapidSSL web page saying "**DOWNLOAD AND INSTALL YOUR CERTIFICATE**". Click on the **Get started** button;
 9. Choose **Microsoft Windows 2012 - IIS 8.0 & 8.5** as our server platform;
 10. Click the **Download** button to receive a zipped file containing the following files.
    **SSLAssistant**: A folder with tool to help installing the cert on IIS, we don't need it.    
    **getting_started.txt**: Optional to read it.    
    **ssl_certificate.p7b**: This is the file we need because it contains the certificates that comprise the "certificate chain" that allows the certificate to be verified up to our CA.
 11. Unzipped the downloaded zipped file.
 12. Get back into **IIS Manager on the same local computer** that created the CSR;
 13. Navigate back to the **Server Certificates** page, and click on **Complete Certificate Request** in the **Actions** pane;
 14. In "Complete Certificate Request" window, browse for the **ssl_certificate.p7b** file;
     - There is a case where we need to select \*.\* as the file name extension in the Open window.
 15. In **Friendly Name** field, enter domain name with a word such as SSL to help distinguish it. Example: "TheWebsiteSSL";
 16. Choose **Personal** for the "**Select a certificate store for the new certificate**" dropdown;
 17. After submission the inputs, the new cert will be listed on the Server Certificates page. Right click on it;
 18. Choose "**Export...**";
 19. Click the ... box to browse to a location where we want to save the PFX file;
 20. Enter password for the PFX file;
 21. Visit the **Certificates** tab of the targeted Cloud Service app in the **Azure Classic Portal**;
 22. Click on "Upload" to upload the PFX file with the password;
     ![Upload cert to Cloud Service](https://info.ssl.com/wp-content/uploads/Upload.png)
 23. Update the **Certificate Thumbprint** in **ServiceConfiguration.Cloud.csfg** and **ServiceConfiguration.Local.csfg** files.
     - Please take note that the **Thumbprint Algorithm** will always be "sha1".
     - Thumbprint Algorithm is used to generate a thumbprint in order to uniquely identify and find a certificate. This algorithm and value is not built into the certificate but is instead calculated whenever a cert lookup is done.
     - Windows, .NET, and Azure all use SHA1 algorithm for the thumbprint algorithm, and SHA1 is the only algorithm allowed in the ServiceConfiguration.cscfg file.
     - Thumbprint Algorithm is **NOT** the **Signing Algorithm** which is used to actually sign the certificate. SHA-1 in Signing Algorithm makes the certificate less secure. So we are not talking about using SHA1 for Signing Algorithm here. Please don't be worried.
  24. Deploy the Cloud Service app to Azure with the new thumbprint for the cert. Done!
 
 ## References
  - [SSL Certificates CSR Creation :: IIS 8 and IIS 8.5](https://www.digicert.com/csr-creation-microsoft-iis-8.htm)
  - [convert p7b to pfx for Azure - Stack Overflow](http://stackoverflow.com/a/14968039/1177328)
  - [Azure Cloud Service and SSL - cuteprogramming](https://cuteprogramming.wordpress.com/2015/03/29/azure-cloud-service-and-ssl/)
  - [Azure Cloud Services only support SHA-1 Thumbprint Algorithm](https://blogs.msdn.microsoft.com/kwill/2015/02/16/azure-cloud-services-only-support-sha-1-thumbprint-algorithm/)
