A user on reddit notes [how scary it is to expose your server to the web](https://www.reddit.com/r/selfhosted/comments/1jiixcx/the_internet_is_scary/). Users give him tips on security : 

* Lots of users recommend using [Cloudflare](https://www.cloudflare.com/en-ca/) and [Crowdsec](https://www.crowdsec.net/).
* They recommend banning certain countries (russia, china, iran, iraq, kuwait, brazil)

Cloudflare, a firewall and fail2ban would solve it. That and IP ban countries you don't need having access.

1. Nginx/Apache/Caddy have lots and lots of use and eyes on the codebase. Big security flaws or just minor fuckups are rare.
2. Using a reverse proxy means you don't need to worry as much about malformed requests. They'll tell the client to fuck off long before sending your app some random bytes rather than a proper HTTP request.
3. You can more easily filter out requests just like this at the reverse proxy very cheaply in terms of compute. That way you don't trigger a potentially resource intensive error in your app.
4. They work readily with things like `crowdsec` or `fail2ban`. There's lots of existing rules for each tailored for httpds.
5. Web servers are awesome at serving static assets and can do their own response caching. Again this saves on resources used by your app.





- **Expose only necessary services**: Don't expose SSH, databases (MongoDB, MySQL, Postgres), or internal tools unless required.
- **Use a reverse proxy**: Nginx, Apache, or Caddy to filter out bad requests before they reach your application.
- **Close unused ports**: Use `nmap` or `netstat` to check for open ports and close anything unnecessary.
- **Geo-blocking**: If your service is region-specific, block countries with high attack rates using Cloudflare or firewall rules.
- **Disable root login**: If using SSH, disable root login (`PermitRootLogin no` in `/etc/ssh/sshd_config`).
- **Use SSH keys** instead of passwords.


### **Backup and Disaster Recovery**
- **Frequent backups**: Store in multiple locations (e.g., local + cloud)
- **Test your backups**: A backup is useless if you can’t restore it.
- **Automate security responses**: Have a "panic button" that shuts down services or revokes compromised credentials automatically.

### **Assume You’ll Get Hacked**
- **Plan for compromise**: Expect a breach at some point.
- **Segment critical data**: Keep backups and sensitive data on separate, isolated systems.
- **Limit privilege escalation**: Use role-based access control (RBAC) and avoid running services as root
- **Regularly update**: Patch OS, applications, and dependencies to prevent known exploits.

### **Use Security-Focused Tools**
- **Cloudflare (or similar)**: DDoS protection, WAF (Web Application Firewall), and bot filtering.
- **OSSEC or Wazuh**: Host-based intrusion detection systems (HIDS).
- **Tailscale or ZeroTier**: Private VPN for secure remote access.
- **Lynis**: Automated Linux security auditing.



### **Network and System Hardening**

- **Harden the Operating System:**  
    Use a minimal install with only necessary packages. Regularly update the OS and installed software. Consider using security modules like SELinux or AppArmor for additional access control.
- **Network Segmentation:**  
    Separate your internal network from public-facing services. Use VLANs or separate physical networks to minimize the damage if one segment is compromised.
- **Isolate Services:**  
    Run services in containers or virtual machines to reduce the risk of lateral movement. If one service is breached, its impact is contained within its isolated environment

### **Access Controls and Authentication**

- **Enforce Two-Factor Authentication (2FA):**  
    For remote access (SSH, VPN, admin panels), require 2FA to reduce the risk of password compromise.
- **Principle of Least Privilege:**  
    Only grant users and services the minimum privileges necessary. Avoid using root or admin accounts for routine tasks.
- **SSH Hardening:**  
    Change the default SSH port, disable password-based logins in favor of key-based authentication, and use tools like Fail2ban to block repeated failed attempts.

### **Monitoring, Logging, and Intrusion Detection**

- **Comprehensive Logging:**  
    Enable detailed logging for all critical systems. Monitor logs for unusual activity using tools like OSSEC or Wazuh.
- **Regular Vulnerability Scanning and Penetration Testing:**  
    Use vulnerability scanners (e.g., Nessus, OpenVAS) to identify weak points and run periodic penetration tests to uncover exploitable vulnerabilities.
- **Intrusion Detection Systems (IDS):**  
    Deploy host-based and network-based IDS to alert you in case of suspicious behavior or intrusion attempts.

### **Data Protection and Backup Strategies**

- **Encrypt Data in Transit and at Rest:**  
    Use TLS for data in transit and consider encrypting sensitive data stored on disk to protect it in case of physical theft or compromise.
- **Frequent and Tested Backups:**  
    Maintain regular backups in multiple secure locations and test your disaster recovery process to ensure data can be restored promptly.

### **Additional Best Practices**

- **Security Awareness and Training:**  
    Educate team members about phishing, social engineering, and the latest security threats. A well-informed team is a critical line of defense.
- **Use a Web Application Firewall (WAF):**  
    In addition to Cloudflare or similar services, a local WAF can provide an extra layer of filtering against common web attacks.
- **Honeypots and Deception Techniques:**  
    Consider deploying honeypots to detect and study malicious activity. These decoys can help you understand attack patterns and refine your defenses.
- **Regular Audits and Compliance Checks:**  
    Periodically review your security policies and configurations. Audits help ensure that all security measures are up-to-date and functioning as expected.