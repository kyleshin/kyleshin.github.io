---
layout: post
title: "Setting Up Custom Domain Name For GitHub Pages"
date: 2018-06-05
comments: false
---
## Setting Up Custom Domain Name For GitHub Pages

Recently I setup a custom domain name for my GitHub Pages, transforming kyleshin.github.io
to www.kyleshin.info. This process is relatively straight forward. I'll detail the steps below.


## 1: Obtain the domain name.
First step is to purchase and register the domain name you want.
I used [Google Domain](https://domains.google/) to purchase and register kyleshin.info.


## 2: Add a CNAME file to your GitHub repository
Go to Your_User_Name.github.io repository (or the appropriate project repository).
Under the settings tab, enter your custom domain name into the Custom domain field, and press save.

![custom domain in settings](/images/blog/2018-06-05/custom_domain_settings.png)

Upon pressing save, GitHub would create a CNAME file in your repository for you. Only the domain you entered
in the field would appear in the CNAME file. So if you need to add another domain (such as apex domain),
you would need to modify the CNAME file.

![CNAME](/images/blog/2018-06-05/cname.png)

**Important!** If you remove the custom domain name from the field, GitHub will automatically remove
the CNAME file as well. I'm bringing this up because you may need to remove the domain name and re-add it again to get the https
certificate to work. More on this later.

## 3: Add CNAME record in DNS.
You'll need to go to your DNS and add a CNAME record.
For either the personal site or project site, you should use Your_User_Name.github.io.
Don't make it an URL, leave out the https://. Otherwise it won't work.

![google dns](/images/blog/2018-06-05/google_dns.png)

![google custom resource record](/images/blog/2018-06-05/google_custom_resource_records.png)


## 4: Enforce HTTPS
At this point, the site should properly be published at the custom domain, but you may need to wait a bit
until you can enforce HTTPS. The duration varies, from 1 hour to maybe 24 hours.

![https ready](/images/blog/2018-06-05/https_ready.png)

It is possible after 24 hours, a message would appear that the certificate cannot be issued. First try
deleting the custom domain from setting(do press save, and this would remove the CNAME), then re-add the
custom domain. This would trigger a new request for certificate. Since a new CNAME file is created, double check it is what you need.

If somehow you are still unable to get a certificate at this point, you would need to contact
GitHub Support.
