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

sudo apt-get install -y git python-dev-is-python3 python3-pil cython3 build-essential

sudo apt install python3-pip

And now, security.  :(  Pip only works in virtual environments.  So, you need to set one up:
python3 -m venv myenv  
source myenv/bin/activate   <--activates virtual env.  Will see on command bar  
pip install git+https://github.com/hzeller/rpi-rgb-led-matrix  
pip install pillow  

Now you need to run with:  
sudo ~/myenv/bin/python matrix_test.py

Okay, close.  Need to disable sound by editing /boot/firmare/config.txt (as sudo).  Change dtparam=audo=on to dtparam=audio=off
Then reboot.

Not quite there.  Need to blacklist the audio driver:
go to /etc/modprobe.d
sudo vi alsa-blacklist.conf
make one line:  blacklist snd_bcm2835

Yay!!!!  Happiness!  

In theory, we can do this *not* in a VM...easier.  
"If you'd rather type sudo python3 script.py like before, you could skip the venv. You'd install with sudo pip install --break-system-packages git+https://github.com/hzeller/rpi-rgb-led-matrix. The name sounds scary, but on a Pi used only for this it's a common shortcut. The venv approach above is the cleaner one."

I'm gonna stick with VMs for now.  Means I need to activate:  
`source myenv/bin/activate`  
and then run with  
`sudo ~/myenv/bin/python <program.py>`  

Image view needed to read directories.  I chmoded it to 755:
chmod 755 /home/pi

needed fonts for spacetank:
sudo apt-get install ttf-mscorefonts-installer

To run on boot: 
* put all commands into a startup.sh file in home.
* chmod this to 777
* sudo crontab -e.  Add bottom of file add:
  `@reboot sleep 15 && /home/pi/startup.sh`

