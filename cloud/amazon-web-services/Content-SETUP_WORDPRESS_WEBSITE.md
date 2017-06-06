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
18. Click the **View Instances** button at the bottom of the page;
19. The virtual machine is ready when its **Instance State** shows "running".
