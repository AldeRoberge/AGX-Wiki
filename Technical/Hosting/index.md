We are using a [Hostinger](https://www.hostinger.com/) provided [Ubuntu](https://ubuntu.com/) Linux dedicated KVM 2 VPS.

The VPS has many roles, especially hosting the [Wiki](https://wiki.aliengarden.com/), [Status](https://status.aliengarden.com/) page, Web and World server.


The server hosts the following services : 

* The [[Technical/Wiki/index|Wiki]] (wiki.aliengarden.com)
* The [[Web Server]] server (testing.aliengarden.com)
* The [[Status]] page (status.aliengarden.com)





#### You need a server

Before starting, ensure you have a VPS. You can buy one from [Hostinger](https://www.hetzner.com/), [Hetzner](https://www.hostinger.com/), [Digital Ocean](https://www.digitalocean.com/), or any cloud provider. You can always [host your own](https://www.reddit.com/r/selfhosted/). I'm using Ubuntu 20.04 on [Hostinger](https://www.hostinger.com/), which costs me about 5$ per month. We'll need it's IP for the following step.


#### You need a domain

I'm using aliengarden.com, a domain I bought on Google Domains (now [Squarespace](https://www.squarespace.com/)) that I pay CA$17 per year. We must add a custom A type record pointing to our server's IP. You can learn more in the [Squarespace Help Center](https://support.squarespace.com/hc/en-us/articles/31119879125645-DNS-records-for-web-hosting) or your domain's provider's help.



#### Install Dockge on your VPS

If this is your first time running this, follow [these steps](https://github.com/louislam/dockge?tab=readme-ov-file#basic) to install Dockge on your machine. Then, we can create the following stack : 





---

## Versioning: Semantic Versioning (SemVer)

Each build follows [[Sementic Versioning (SemVer)]]: `MAJOR.MINOR.PATCH` 