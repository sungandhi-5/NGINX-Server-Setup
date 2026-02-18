## 1. Before Installing Nodejs, Update and Upgrade your ubuntu system

```
sudo apt update && sudo apt upgrade -y
```
## 2. Install necessary dependencies

```
sudo apt install -y ca-certificates curl gnupg
```
## 3. Import GPG key for the source
With our required packages installed, we’ll go ahead and import the GPG key for NodeSource’s repository:
```
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
```
## 4. Add the APT source
Next, we’ll add the APT source for Node.js 22. If you happen to want a different version of Node.js, you can adjust the 22.x in the echo statement:
```
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_22.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
```

## 5. Update and install
With the source repository added, we’re ready to install the package. First, we need to run another update to sync the package list, then we can proceed with installing Node.js 22:
```
sudo apt update && sudo apt install nodejs -y
```

## 6. Check the version
- To install the latest stable version, run following command :
```
node --version
```





## Installing nodejs using NVM
- NVM is the Node Version Manager, which allows you install multiple versions of Node.js and bounce between them depending on the project.

## 1. Installing NVM

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
```

```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

## 2. Installing Node.js 21 via NVM
To install Node.js 21, run:

```
nvm install 21
```

- if this is the very first version of Node.js you’re adding with NVM, it should set it as the default version for you automatically, and you should be good to go.
- Otherwise, if this is a new version of Node.js being added, or if for some reason your version of NVM doesn’t automatically create the alias, you can run:

```
nvm alias default 21
```

- If you switch betweem nodejs version, use below command:

```
nvm install 22
nvm use 22
```
