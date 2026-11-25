# pi_2026

These are my notes for getting a pi 3 back up and going using the RGB matrix library.

First, download and install the raspberry pi imager from here:
https://www.raspberrypi.com/software/

Installed a headless OS (no desktop enviornment).  I didn't do all the network gunk....gonna do that by hand.

then, raspi config for ssid and hostname

python3 already installed

git:  
sudo apt update
sudo apt install git -y

generated SSH key for github:
ssh-keygen -t ed25519 -C "g.salaman@comcast.net"

Hit enter through all prompts...no passphrase.

Then do a cat on your key so you can copy it:
cat ~/.ssh/id_ed25519.pub
To add to github:
* Log into github from browser.
* Click profile picture, settings.
* In left sidebar, click SSH and GPG keys.
* Click grenen "NEW SSH key" button
* Give it a recognizable title, paste the copied key, and click "Add SSH key"

To test:
ssh -T git@github.com

To clone:
git clone ssh://git@github.com/[username]/[repository-name].git

Cheat sheet is here:
https://github.com/joshnh/Git-Commands

Okay, so far so good...but I need the hzellar library

