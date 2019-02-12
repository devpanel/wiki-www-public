---
title: Linking to AWS
taxonomy:
    category: docs
    tag: docs
process:
  twig: true
---

1. In a devPanel Workspace, click "Create Server".

![](01.jpg)

2. Note that the "Create Server" button is now disabled... that's because the Provisioner is not configured yet.

![](02.jpg)

3. Let's configure the Provisioner next... click "Configure Provisioner".

![](03.jpg)

4. Your page will look like this.

![](04.jpg)

Leave this page as is for now.

5. Login to your AWS Console and select IAM service.

![](05.jpg)

6. Click on Users.

![](06.jpg)

7. Click on Add user button.

![](07.jpg)

8. Enter a user name, for example "devpanel"; Give it Programmatic access and click Next.

![](08.jpg)

9. Under the "Add user to group", search and select the "admin" group, click Next.

![](09.jpg)

10. Review and make sure everything looks right… then click Next.

![](10.jpg)

11. You should get a Success message.

![](11.jpg)

12. Copy and paste the Access key and Secret key from AWS to devPanel.

![](12a.jpg)

![](12b.jpg)

13. Click the Save button on devPanel.

![](13.jpg)

14. Click the Close button on AWS.

![](14.jpg)

15. Your Provisioner is now setup on devPanel and you're now free to create a server in your Workspace.

![](15.jpg)
