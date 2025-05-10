## Host your website 

- login to your server 

1. create your project directory at below location 

```
sudo mkdir /usr/share/nginx/<PROJECT_NAME>
```
```
sudo chmod -R 755 /usr/share/nginx/<PROJECT_NAME>
```

2. Create site configuration file

- First, remove default configuration file to avoid conflicts

```
sudo rm /etc/nginx/sites-available/default
```

- Now create your site's configuration file

```
sudo nano /etc/nginx/sites-available/<DOMAIN_NAME>.conf
```
- Paste this below code, to run website on IP

```
server{
    listen 80;
    server_name _;
    include /etc/nginx/mime.types;
    location / {
           proxy_pass http://127.0.0.1:3000;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_cache_bypass $http_upgrade;
           proxy_redirect off;
           proxy_http_version 1.1;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Port "443";
           proxy_set_header X-Forwarded-Proto "https";
          # proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
- If you want to run your website on domain than make following changes change

```
server_name <DOMAIN_NAME> www.<DOMAIN_NAME>
```
Save the file

3. Enable the Site in Nginx
Create a symbolic link from the configuration file to the sites-enabled directory:

```
sudo ln -s /etc/nginx/sites-available/<DOMAIN.COM> /etc/nginx/sites-enabled/
```

4. Check Nginx Configuration and Restart
Check the Nginx configuration for any syntax errors:

```
sudo nginx -t
```

```
sudo systemctl restart nginx
```










