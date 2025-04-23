
## 1. Update Linux Packages And Install mysql-server

```
sudo apt-get -y install nginx mysql-server
```
## 2. Set Mysql Root User Password

```
sudo mysql -u root
```
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'ROOT_PASSWORD';
```
```
exit;
```
## 3. Secure MySQL Installation

- This step will help set the root password and remove insecure defaults.
```
sudo mysql_secure_installation
```
- You'll be prompted to:
1. Set up the root password : Enter password that your set in previous step
2. Remove anonymous users : Yes
3. Disallow remote root login : No
4. Remove test databases : Yes
5. Reload privilege tables : Yes

## 4. Check If MySQL Is Running

```
sudo systemctl status mysql
```
- If not started than,run below command
```
sudo systemctl start mysql
```
- Optional : Enable MySQL to start on boot
```
sudo systemctl enable mysql
```

## 5. Login To MySQL

```
sudo mysql
```
- If you set a password and want to log in with it:
```
mysql -u root -p
```
