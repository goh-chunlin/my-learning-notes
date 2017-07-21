# Enable Users Access To Billing Console

Most of the time, even after an administrator sets appropriate permissions for an IAM user to access the Billing Console, the user still cannot access the Billing Console. This is because access to the Billing Console requires additional step.

## Enable IAM User Access to Billing Console
After granting IAM users permissions to the Billing Console, the AWS account owner (Other IAM users, even with full permissions, cannot get to this page) needs to go to the [**Account Settings**](https://console.aws.amazon.com/billing/home#/account) page for the account using the root password.

On the account settings page, there's a section titled **IAM User Access to Billing Information**. The account owner should click the **Edit** button, check the **Activate IAM Access** check box, and then click the **Update** button.

After access has been enabled, IAM users in the account who have been granted appropriate permissions can view and work with the Billing Console.

## Reference
[Don't Forget to Enable Access to the Billing Console! - AWS Security Blog](https://aws.amazon.com/blogs/security/dont-forget-to-enable-access-to-the-billing-console/)
