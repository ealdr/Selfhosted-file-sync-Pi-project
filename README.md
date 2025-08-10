# Selfhosted-file-sync-Pi-project

This README contains a complete write-up of the steps and processes I did to set up and run a fully encrypted, self-hosted file synchronization system on a Raspberry Pi 5 using Syncthing. It documents the problem that led to the project, the hardware and software used, the installation and configuration process, and the final outcome.

---

## Why I Started This Project - The problem I was having

I created this self-hosted file synchronization system to solve a challenge I faced during my Computer Science NEA. We were allowed to bring in our own portable computers and use an IDE of our choice — mine being PyCharm, which is not available on the school system. Since I only have a desktop PC and an iPad (which cannot run Python and Tkinter due to App Store restrictions), I needed an alternative solution.

To work around this, I set up remote access to my Raspberry Pi from sixth form using Pi Connect, allowing me to code on it directly. I then added automated, encrypted file synchronization between the Pi and my desktop PC using Syncthing, eliminating the need to repeatedly upload files to Google Drive or other cloud storage services.
