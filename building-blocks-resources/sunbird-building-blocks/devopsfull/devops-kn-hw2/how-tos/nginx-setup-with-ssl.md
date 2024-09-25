---
icon: elementor
---

# Nginx setup with ssl:

1. Generate certificate from:

[![](https://punchsalad.com/wp-content/uploads/2020/09/cropped-Icon-profile-2-32x32.png)SSL Certificate Generator: Free letsencrypt SSL in minutes - PunchSalad](https://punchsalad.com/ssl-certificate-generator/)

<figure><img src="../../../../../.gitbook/assets/generate-ssl-cert.png" alt=""><figcaption></figcaption></figure>

&#x20;

2. Update DNS record , wait for 5 mins and check the dns ex:



<figure><img src="../../../../../.gitbook/assets/update-dns-record-ssl2.png" alt=""><figcaption></figcaption></figure>

&#x20;

3. Once record is verified , download the cert from next page



<figure><img src="../../../../../.gitbook/assets/download-ssl-cert.png" alt=""><figcaption></figcaption></figure>

&#x20;

4. rename the files accordingly

`sudo mv your_domain_chain-CA.txt your_domain_chain.crt sudo mv your_private-key.txt your_private.key`

5. Install nginx

`sudo apt update sudo apt install nginx`

6. create directory to store ssl certs and copy the downloaded cert files in Step 4

`sudo mkdir /etc/nginx/certs`

7. Create a nginx configuration file

`vi /etc/nginx/sites-available/mysite.confserver { listen 80; server_name $domainname; # update this return 301 https://$server_name$request_uri; #redirect to https } } server { listen 443 ssl; ssl_certificate /etc/nginx/certs/your_domain_chain.crt; # update this ssl_certificate_key /etc/nginx/certs/your_private.key; # update this server_name your_domain.com; # update this location / { proxy_pass http://localhost:8080; } }`

8. Create symlink

`sudo ln -s /etc/nginx/sites-available/dev-allbot.conf /etc/nginx/sites-enabled/`

9. check configuration and reload nginx

`sudo nginx -t && sudo nginx -s reload`

&#x20;
