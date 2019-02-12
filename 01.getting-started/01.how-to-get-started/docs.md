---
title: 'How to get started'
taxonomy:
    category: docs
    tag: docs
---

1. Get an account on AWS (if you don't have one already)
2. Get an account on github.com (if you don't have one already)
3. Login to devPanel using your github account (highly recommended)
4. Create a new Workspace (workspaces are fully self-contained projects) you can create as many as you like
5. Go into your workspace and click on "Create Server"
6. Click "Configure Provisioner." Provisioners are how we access your AWS account. The credentials that you provide here are kept securely in a digital vault.
7. On AWS, create a new IAM user, called 'devPanel' for example, with admin programmatic access (devPanel uses the AWS API). [See step-by-step instructions](/help/tutorial)
8. Copy & paste the “Access Key” and “Secret Key” from AWS into devPanel and Save it
9. That's it... you're done creating your AWS provisioner on devPanel
10. You can now create as many servers as you want in that devPanel workspace

> Notes & Tips
> * Note: You'll have to setup a provisioner for each new Workspace/Project
> * Tip: Create a new IAM user for each Workspace/Project
> * Tip: If you're doing work for a client, create the IAM user under their AWS account. That way, they get billed by AWS directly
