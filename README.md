# VBox_Ubuntu_NodeRED_MongoDB_OpenPLC
Instructions for preparing a VirtualBox Image with Ubuntu Desktop + Node-RED + MongoDB (via Docker) + OpenPLC

Install the latest Oracle VirtualBox (https://www.virtualbox.org/)

#### Note: Windows 10 Pro and Enterprise users need to disable Hyper-V in order to make VirtualBox works (See https://support.microsoft.com/en-au/help/3204980/virtualization-applications-do-not-work-together-with-hyper-v-device-g)
 
## Install Raspbian Desktop into a Virtual Machine

Under **Oracle VM VirtualBox Manager**, Click **[New]**

 * Enter **Ubuntu VM** as the name
 * Select **Linux** under the **Type** pull-down menu
 * Select **Ubuntu (64-bit)** under the **Version** pull-down menu
 * Allocate **4096 MB** of memory to the virtual machine

Click **[Create]**

 * Allocate **25 GB** to the Virtual Hard Disk
 * Check **VDI (VirtualBox Disk Image)**
 * Check **Dynamically allocated**
 
Click **[Create]**

Under **Oracle VM VirtualBox Manager**, Click **[Settings]**

 * Select **System**, select **Processor**, set **Processor(s)** to 2 or higher
 * Select **Display**, set **Video Memory** to 32 MB or higher
 * Select **Storage**, select **Empty** under **Controller: IDE**
 * Click the **CD** icon next to **Optical Drive**, select the latest Ubuntu Desktop LTS image file (https://ubuntu.com/download/desktop)

Click **[OK]**

Under **Oracle VM VirtualBox Manager**, Click **[Start]**

Select **Try or Install Ubuntu** from the bootup menu and follow the on-screen instructions

## Install the display driver

Once Ubuntu Desktop is installed, from the toolbar of the VirtualBox window on the **Host PC**, select **Devices --> Insert Guest Additions CD image**

Then, on **Ubuntu Desktop**, open a Terminal (right-click on desktop --> terminal), type 
```
sudo sh /media/$UID/VBox_GAs_6.1.40/VBoxLinuxAdditions.run
sudo reboot
```
Note: change **$UID** to your username

## Install Curl

In the Terminal, type
```
sudo apt-get install curl
```

## Install Node.js

Follow the instructions to install Node.js (https://github.com/nodesource/distributions/blob/master/README.md#debinstall). The following is for installing Node.js v18.x

In the Terminal, type
```
curl -fsSL https://deb.nodesource.com/setup_19.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```

## Update NPM

The following is for updating NPM to version 9.2.0. In the terminal, type
```
sudo npm install -g npm@9.2.0
```

## Install Node-RED

In the Terminal, type
```
sudo npm install -g --unsafe-perm node-red
```

### Start Node-RED

In the Terminal, type
```
node-red
```

## Install extra nodes

Open a browser and type http://127.0.0.1:1880

* Click the **Three Strips** icon on the top-right corner
* Select **Manage palette** 
* Select the **Install** Tab, search with the keyword **aedes** 
* Install **node-red-contrib-aedes (https://flows.nodered.org/node/node-red-contrib-aedes)** (v. 0.9.0) 
* search with the keyword **dashboard**
* Install **node-red-dashboard (https://flows.nodered.org/node/node-red-dashboard)** (v. 3.2.3)

## Install emulators

Follow the instructions in (https://github.com/ctch3ng/Node-red-inputs-emulators) to install the emulators

## Install MongoDB (via Docker) and Mongo-Compass

Follow the instructions in (https://docs.docker.com/engine/install/ubuntu/) to install Docker Engine

In the Terminal, type
```
mkdir mongo-data
sudo docker run -d -p 27017:27017 --name mongo-database -v mongo-data:/data/db mongo:4.4
```
Note: Version 4.4 is used as the more recent versions require CPU that support amd64-avx and will terminate immediately with an exit code 132

Following the instructions here (https://www.mongodb.com/docs/compass/current/install/) and install Mongo-Compass

## Install OpenPLC Editor and Runtime

Download (https://openplcproject.com/download/) and follow the instructions in the README.md to install the editor
Note: you may need to edit the install.sh and hardcode the path to your /home/@UID/.local/share/applicaitons

Follow the instructions here (https://openplcproject.com/docs/installing-openplc-runtime-on-linux-systems/) and install the Runtime
