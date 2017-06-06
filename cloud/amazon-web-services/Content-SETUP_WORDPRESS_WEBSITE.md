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
4. Copy the URL into a new tab in the web browser, and we should see a default Wordpress website.

## Login to Wordpress Backend
1. Once the instance is running, we can now test our WordPress website;
2. Tick the instance checkbox;
3. Read carefully the **AWS Marketplace Usage Instructions** for the instance in its **Usage Instructions** tab;
4. Click on the **Action** button on the top of the page;
5. Choose **Instance Settings > Get System Log**;
6. In the **System Log** popup window of the instance, scroll down to near the bottom of the long text to look for the words **AWS Marketplace Usage Instructions** which is surrounded by hash marks;
7. Copy the password (without the quotes);
8. Click the **Close** button;
9. Now that we have the password, switch back to the WordPress Hello World page. Add /wp-admin to the end of the URL so it looks something like http://xxxxxxxxx.yyyyyyyy.compute.amazonaws.com/wp-admin. Hit enter;
10. As shown in the **Usage Instructions** in the **Step 3**, enter the Username **user** and the Password that we get in **Step 7**;
11. Proceed to login;
12. We are now login to the backend of our Wordpress website;
13. **DO NOT CHANGE** the password of the admin user unless you know what you are doing.
