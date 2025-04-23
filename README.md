## 1. Update Linux Packages

```
sudo apt-get update -y
```
## 2. Install Nginx

```
sudo apt-get -y install nginx
```
## 3. Check Nginx Configuration Is Ok!
```
sudo nginx -t
```
## 4. Start Nginx
```
sudo systemctl start nginx.service
```
## 5. Check Nginx Status
```
sudo systemctl status nginx.service
```
