<div style="text-align:center"><img src="logo.png" /></div>

# adMooH Linux Packages

## Ubuntu 16.04 x64
## **Register adMooH key and feed**

Before installing adMooH Server, you'll need to register the adMooH key, register the product repository. This only needs to be done once per machine.

Open a terminal and run the following commands:

```sh
wget -qO - https://raw.githubusercontent.com/adMooH/admooh-linux-packages/master/PUBLIC.KEY | sudo apt-key add -
echo "deb https://raw.githubusercontent.com/adMooH/admooh-linux-packages/master/ bionic main" | sudo tee /etc/apt/sources.list.d/admooh.list
```

## **Install adMooH AD Server**

Update the products available for installation, then install the adMooH AD Server.

In your terminal, run the following commands:

```sh
sudo apt-get update
sudo apt-get install admoohserver
```

## **Setup Startup**

Create a .startup file and set it to executable. 

In your terminal, run the following commands:
```sh
cd $HOME
touch admooh.startup
sudo chmod +x admooh.startup
nano admooh.startup
```

Paste this into the editor and save:

```txt
sudo apt-get --only-upgrade install admoohserver
cd /opt/admooh
sudo ./Admooh.Agent.Server
```

Now you need to have admooh.startup run on startup so you can use cronjob as sudo.

In your terminal, run the following commands:

```sh
sudo su
crontab -e
```

and paste:
\* Remember to exchange $USER_NAME for username !!!

```
@reboot /usr/bin/sudo /home/${USER_NAME}/admooh.startup
```

