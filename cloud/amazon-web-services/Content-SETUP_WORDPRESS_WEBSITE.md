# Setup Wordpress Website on Amazon EC2 Virtual Machine

## Background
1. We will be using an existing Amazon Machine Image (AMI) from the AWS Marketplace that has WordPress already installed.

## Configure EC2 Instance
1. Login to the **[AWS Management Console](https://console.aws.amazon.com)**;
2. Go to the **EC2 Management Console**;
3. Select the appropriate **AWS Region** at the top-right corner of the website;
4. Click **Launch Instance** button from the dashboard to create the virtual machine;
5. Click on **AWS Marketplace** on the left-hand side, search for **WordPress powered by BitNami**, then click **Select** button;
6. Since the "WordPress powered by BitNami" is **Free tier eligible**, by default the instance selected will be **t2.micro (Free tier eligible)**. Leave it as it is and click **Next: Configure Instance Details** button;
7. Change nothing and click **Next: Add Storage** button;
8. Change nothing and click **Next: Add Tags** button;
9. Create a new tag with the "Name" as **Name** and "Wordpress-Happenings" (This needs to be very easy-to-understand to the developers) as **Value**;
10. Click **Next: Configure Security Group** button;
11. Set the **Source** of the **SSH** record to be **My IP** so outsider's traffic cannot SSH to our virtual machine;
12. Click **Review and Launch** button;
13. Review the configurations, then click **Launch** button;
14. In the **Select an existing key pair or create a new key pair** popup window, choose **Create a new key pair** and enter a meaningful and easy-to-understand **Key pair name**;
15. Click **Download Key Pair** button;
16. Save the downloaded file in a secured place;
17. Click the **Launch Instances** button;
18. Click the **View Instances** button at the bottom of the page (there may be a need to scroll down to see it);
19. The virtual machine is ready when its **Instance State** shows "running".

## Test the Wordpress Website, Hello World!
1. Once the instance is running, we can now test our WordPress website;
2. Tick the instance checkbox;
3. Find the **Public DNS (IPv4)** for the instance in its **Description** tab;
4. Copy the URL into a new tab in the web browser, and we should see a default Wordpress website;
5. Take note of the **Private IPs** (there should only be one record) in the Description tab as well for later use.

## Login to Wordpress Backend
1. Once the instance is running, we can now test our WordPress website;
2. Tick the instance checkbox;
3. Read carefully the **AWS Marketplace Usage Instructions** for the instance in its **Usage Instructions** tab;
4. Click on the **Actions** button on the top of the page;
5. Choose **Instance Settings > Get System Log**;
6. In the **System Log** popup window of the instance, scroll down to near the bottom of the long text to look for the words **AWS Marketplace Usage Instructions** which is surrounded by hash marks;
7. Copy the password (without the quotes);
8. Click the **Close** button;
9. Now that we have the password, switch back to the WordPress Hello World page. Add /wp-admin to the end of the URL so it looks something like http://xxxxxxxxx.yyyyyyyy.compute.amazonaws.com/wp-admin. Hit enter;
10. As shown in the **Usage Instructions** in the **Step 3**, enter the Username **user** and the Password that we get in **Step 7**;
11. Proceed to login;
12. We are now login to the backend of our Wordpress website;
13. **DO NOT CHANGE** the password of the admin user unless you know what you are doing.

## Associate Elastic IP Address and Custom Domain Registration
1. In the left panel of the EC2 Management Console, click on the **Elastic IPs** under the **NETWORK & SECURITY**;
2. Click the **Allocate New Address** button;
3. Click the **Allocate** button;
4. A green message will be displayed saying "**New address request succeeded**";
5. Copy the **Elastic IP**;
6. Click the **Close** button;
7. Tick the new IP address checkbox;
8. Click the **Actions** button and choose the **Associate Address** option;
9. Select the virtual machine in the **Instance** dropdown and search for the **Name** we entered in the **Step 9** of "**Configure EC2 Instance**";
10. Select the IP address we saw in the **Step 5** of "**Test the Wordpress Website, Hello World!**" in the **Private IP** dropdown;
11. Click **Associate** button;
12. Click **Close** button when there is a green message "**Associate address request succeeded**" displayed;
13. Verify that the new Elastic IP address is working by typing it (the IP we got in the **Step 5**) into our web browser and we should see the same Wordpress website;
14. Login to the Internet domain registrar, eg. GoDaddy;
15. Create a new **A Record** under our domain name pointing to the Elastic IP created in **Step 5** (This step will take a while for the domain name to point to the Elastic IP).

## Connect to the Instance from Windows Using PuTTY to Remove Bitnami Logo
1. On the Wordpress website, there will be a Bitnami logo shown in the bottom-right of the page. We can remove it by access to our virtual machine first using PuTTY ([Download Here](https://www.chiark.greenend.org.uk/~sgtatham/putty/));
2. Start **PuTTY Key Generator** (for example, from the Start menu, choose All Programs > PuTTY > **PuTTYgen**);
3. Under **Type of key to generate**, choose **SSH2-RSA**;
4. Click the **Load** button. By default, PuTTYgen displays only files with the extension .ppk. To locate our .pem file generated in the **Step 16** of **Configure EC2 Instance**, select the option to display files of all types;
5. Choose **Save private key** to save the key in the format that PuTTY can use. PuTTYgen displays a warning about saving the key without a passphrase. Choose **Yes**;
   - **NOTE** A passphrase on a private key is an extra layer of protection, so even if the private key is discovered, it can't be used without the passphrase. The downside to using a passphrase is that it makes automation harder because human intervention is needed to log on to an instance, or copy files to an instance.
6. Save the .ppk file using the **SAME FILE NAME** as we used for the .pem file in the **Step 16** of **Configure EC2 Instance**;
7. Keep both the .pek file in secured place;
8. Start **SSH, Telnet, and Rlogin client** (for example, from the Start menu, choose All Programs > PuTTY > **PuTTY**);
9. In the **Category** left panel, select **Session** and complete the following fields:
   - Host Name: **bitnami@[Public DNS Name]** (The user name is bitnami as shown in the **Step 3** of **Login to Wordpress Backend**. The Public DNS Name may be **NO LONGER THE SAME** as the Public DNS shown in the **Step 3** of **Test the Wordpress Website, Hello World!**. Please revisit the **Description** tab of the virtual machine to get the new one);
   - Port: **22**
   - Connection type: **SSH**
   - Saved Session: **[Meaningful Name]**
10. In the **Category** left panel, expand the **SSH** option under **Connection** and then select **Auth**;
11. Click on the **Browse** button;
12. Open the .ppk file generated in the **Step 6**;
13. **DO NOT CLICK** the **Open** button at the bottom;
14. In the **Category** left panel, select **Session** and click the **Save** button;
    - **NOTE** Next time we can just directly **Load** from the saved Session instead of repeating the steps above to access the virtual machine.
15. Click the **Open** button at the bottom;
16. We are now logged in to the virtual machine;
17. Execute the following command;
    ```
    sudo /opt/bitnami/apps/wordpress/bnconfig --disable_banner 1
    ```
18. Once the command above is executed, restart the Apache server with the following command;
    ```
    sudo /opt/bitnami/ctlscript.sh restart apache
    ```
19. Once the Apache server is restarted, revisit the Wordpress blog. The Bitnami logo will be gone.

## References
- [Launch a WordPress Website](https://aws.amazon.com/getting-started/tutorials/launch-a-wordpress-website/)
- [Register a Domain Name](https://aws.amazon.com/getting-started/tutorials/get-a-domain/)
- [Connecting to Your Linux Instance from Windows Using PuTTY](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html)
- [Bitnami WordPress For AWS Cloud](https://docs.bitnami.com/aws/apps/wordpress/)
- [How can I remove bitnami banner on wordpress site - Stack Overflow](https://stackoverflow.com/a/34748576/1177328)
- [Documentation For Bitnami Info Page](https://docs.bitnami.com/general/components/bninfo/)
