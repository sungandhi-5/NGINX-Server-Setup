## 1. Update Linux Packages

```
sudo apt-get update -y
```
## 2. Check Linux Version

```
cat /etc/lsb-release
```
## 3. Import The Public Key.
From a terminal, install gnupg and curl if they are not already available:
```
sudo apt-get install gnupg curl
```
To import the MongoDB public GPG key, run the following command:
```
curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
   --dearmor
```
## 4. Create The List File.
Create the list file /etc/apt/sources.list.d/mongodb-org-8.0.list for your version of Ubuntu.

- Ubuntu 24.04 (Noble)
```
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
```
- Ubuntu 22.04 (Jammy)
```
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
```
- Ubuntu 20.04 (Focal)
```
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
```

## 5. Reload the package database.
```
sudo apt-get update -y
```

## 6. Install MongoDB Community Server.
- To install the latest stable version, issue the following
```
sudo apt-get install -y mongodb-org
```
- To install a specific release, you must specify each component package individually along with the version number.
```
sudo apt-get install -y \
   mongodb-org=8.0.6 \
   mongodb-org-database=8.0.6 \
   mongodb-org-server=8.0.6 \
   mongodb-mongosh \
   mongodb-org-shell=8.0.6 \
   mongodb-org-mongos=8.0.6 \
   mongodb-org-tools=8.0.6 \
   mongodb-org-database-tools-extra=8.0.6
```

## 7. Reload Deamon
```
sudo systemctl daemon-reload
```
## 8. Start MongoDB
```
sudo systemctl start mongod
```
## 8. Status MongoDB
```
sudo systemctl status mongod
```
- You can optionally ensure that MongoDB will start following a system reboot by issuing the following command:
```
sudo systemctl enable mongod
```
## 9. Stop MongoDB
```
sudo systemctl stop mongod
```
## 10. Restart MongoDB
```
sudo systemctl restart mongod
```
## Add Authentication to Database

```
mongosh
```
```
use admin
```
- Create a New Admin User with Password

```
db.createUser({
  user: "admin",
  pwd: "yourStrongPassword",
  roles: [ { role: "root", db: "admin" } ]
});
```
Here,
- user: "admin" , Username.
- pwd: "yourStrongPassword" -> Password you want.
- role: "root" -> Full permission over all databases.
- db: "admin" -> Role is assigned inside the admin database.

- If you create user for specific database with only read,write permission then use below command :

```
db.createUser({
  user: "myUsername",
  pwd: "myPassword",
  roles: [
    { role: "readWrite", db: "yourDatabaseName" }
  ]
});
```

- Enable Authentication in mongod.conf
``` 
sudo nano /etc/mongod.conf
```
- Uncomment **security:** key and add line like below :

```
security:
  authorization: "enabled"
```

- Restart mongodb
```
sudo systemctl restart mongod
```
