## Produced by the group 4 idiots

First, make sure you have pnpm tools, if not follow the steps below:
1. make sure your node version can install pnpm:
   see in https://pnpm.io/installation#compatibility , if your node version doesn't support the pnpm tool, it is recommend to use nvm tool to manage the node. Below steps works on Windows, for Macos, you need to         search online, because we don't have mac, we don't know which can works correctly.
   1.1 uninstall your current node
     Open the Control Panel -> Open Programs and Features -> Search for "node" in the upper right corner -> Right-click to uninstall
   1.2 go to https://github.com/coreybutler/nvm-windows/releases to install nvm
     install nvm-setup.zip
   1.3 type "nvm version" in terminal to see if the nvm is installed correctly.
   1.4 type "nvm list available" to see the versions that can be installed on the network.
   1.5 Select a version for installation, such as "nvm install 14.14.0"
   1.6 Use this version of node, "nvm use 14.14.0". Entering "node -v" and "npm -v" can query the version numbers of node and npm.
   1.7 Type "npm install -g pnpm" to install pnpm tools


Then, install dependencies, type the instruction below in project root libary:

```bash
pnpm install

#or

pnpm i
```

After installing:

```bash
pnpm dev
```

to run the project. The project will run on localhost:3000, Make sure the port is not occupied. Otherwise the project will not run.

You need to wait a moment the first time you run the project, otherwise the project will encounter some issues due to insufficient loading. After full loading, no problems will occur.

If you have any problems, you can send email to me directly: xli22@student.oulu.fi(university email, but I recommend send to personal email, because I may mistake it as an advertisement),  shawnlee0803@163.com(personal email).
Wechat account: \_\_ShawnLee\_\_ (double _ both in the front and rear)
