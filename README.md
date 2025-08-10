# Selfhosted-file-sync-Pi-project

This README contains a complete write-up of the steps and processes I did to set up and run a fully encrypted, self-hosted file synchronization system on a Raspberry Pi 5 using Syncthing. It documents the problem that led to the project, the hardware and software used, the installation and configuration process, and the final outcome.

---

## Why I Started This Project - The problem I was having

I created this self-hosted file synchronization system to solve a challenge I faced during my Computer Science NEA. We were allowed to bring in our own portable computers and use an IDE of our choice — mine being PyCharm, which is not available on the school system. Since I only have a desktop PC and an iPad (which cannot run Python and Tkinter due to App Store restrictions), I needed an alternative solution.

To work around this, I set up remote access to my Raspberry Pi from sixth form using Pi Connect, allowing me to code on it directly. I then added automated, encrypted file synchronization between the Pi and my desktop PC using Syncthing, eliminating the need to repeatedly upload files to Google Drive or other cloud storage services.

---

## What is Syncthing
Syncthing is a free file synchronization service which allows you to share files across a load of different computers, with a peer to peer method rather than client to server method. Allows you to mirror folders across computers.

---

## Hardware and Software I used

- Raspberry Pi 5 (8gb)
- Raspberry Pi OS (64-bit)
- Pi connect
- Syncthing
- Pycharm

---

## Installation Process

First I installed the latest [Pi OS](https://www.raspberrypi.com/software/) version onto the SD card via my PC and the Imager application.

To install Pi-connect I ran the following commands: `sudo apt update` and `sudo apt full-upgrade`. After everything was checked and installed I then ran `sudo apt install rpi-connect` which installed Pi connect itself. I then logged into my Pi connect account to enable me to connect remotly from my desktop or Ipad without the need for the Pi to be plugged into a screen.

### Syncthing

To start the install of [Syncthinhg](https://syncthing.net/), in the command prompt I ran `sudo apt install syncthing` which installs everything I need. Then I run syncthing for first time via `syncthing` which setups up everything ready for later. To stop it again I pressed `Ctrl + C`.
To be able to access the web GUI I needed to change the .config file in the Sync folder. So I ran `ls` to find the sync folder on my Pi. Once I found it, I ran `sudo vim .config/syncthing/config.xml`. In the config file I went to find `<gui`, under address and changed the IP to `0.0.0.0:8384` to allow any device on my network able to access it. Also making sure my router is not forwading the port to outside the firewall.

I then exited and saved the nano .config edits, back to the comnmand promt i ran  `syncthing` again, this time I am able to access it from my web browser by typing `raspberrypi.local:8384`

On the browser GUI it prompted me to setup a GUI authentication username and password, which I did.

I then installed [Syncthing's Windows app](https://syncthing.net/downloads/) to add a computer to the Syncthing file sharing network. Once I had installed it 2 new icons appear in the start menu, one for start and one for stop. I clicked start and it automattically opens the Desktop IP GUI on the web browser because im still on the local network.

---
## Setting up and connecting 

On the new tab that opened I clicked add remote device, it then asks for a device ID. So I went back into the Raspberry Pi browser tab, went to Actions > Show ID, then at the top there was a long string of characters or a QR code so I copied the ID and pasted it back into the Desktop tab. Then under sharing I checked the box which said Introducer which means it can share folders with the Desktop. When going back onto the Pi there was a request for the new device to connect, making sure it was my desktop I clicked  '+ Add Device'.

Before adding any data, I made sure everything was secure by going to Actions > Settings > Connections and disabled NAT transversal and Global discovery on both Desktop and Pi, so only local people could connect to it. For the changes to take place I restarted Syncthing on both sides.

I created a new folder called Shared Code, and in the settings check the box which says 'Share with Desktop'. Under advanced I changed the full scan interval to every 1 hour rather than the defualt 30 minutes and clicked save.

Back on the desktop tab there was a request which said 'Pi wants to share a folder with desktop', I clicked 'Add' and under folder path put the shared code folder under my pre-existing code folder on my computer.

---

## Testing 

On my desktop I added a .txt document called 'test' to the 'Shared Code' folder in file explorer, and then forced a rescan on the GUI. Went back to my raspberry Pi screen sharing on Pi connect opened the folder and it had successfully worked.

<img width="200.5" height="100.5" alt="image" src="https://github.com/user-attachments/assets/d84f88c1-b6cd-4301-9a9b-4625868c4ff5" />


For syncthing to open when the Pi comes online I had to enable the syncthing service, by running `sudo systemctl enable syncthing@pi.service`. I then rebooted the Pi, went to the web browser GUI to see that syncthing started up on its own after the restart.

---

## Pycharm

To install the IDE [Pycharm](https://www.jetbrains.com/pycharm/) I went to the [Downloads](https://www.jetbrains.com/pycharm/download/?section=linux) page on their website, and selected linux as Pi OS is a debian based Linux distribution. Once I had downloaded the the .tar.gz file, I extracted it and then executed the `Pycharm.sh` file. To make it so I dont have to go to the file everytime I want to use Pycharm, when it opened I clicked in the bottom left create desktop shortcut, which added it to the programming section in my Pi.











<img width="520" height="236" alt="image" src="https://github.com/user-attachments/assets/83fa4915-3865-4f7a-8677-11e71ee50108" />

