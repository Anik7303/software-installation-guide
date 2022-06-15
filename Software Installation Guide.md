# Software Installation Guide for `ubuntu`:

## Contents

- [Nvidia Driver](#nvidia-driver)
- [Google Chrome](#google-chrome)
- [Git](#git)
- [Github CLI](#github-cli)
- [VLC Media Player](#vlc-media-player)
- [H264 Decoder](#h264-decoder)
- [Visual Studio Code](#visual-studio-code)
- [NodeJS](#nodejs)
- [MongoDB Community Edition](#mongodb-community-edition)
- [Docker](#docker)
- [Anaconda](#anaconda)
- [KVM](#kvm)
- [ZSH Shell](#zsh-shell)
- [Deluge](#deluge)
- [JAVA](#java)
- [Android Studio](#android-studio)
- [Qbittorrent](#qbittorrent)
- [youtube-dl](#youtube-dl)
- [uGet Download Manager](#uget-download-manager)
- [uGet-integrator](#uget-integrator)
- [XDM - Xtreme Download Manager](#xdm-xtreme-download-manager)
- [Ohter Softwares](#other-softwares-download-from-website)

## Nvidia Driver

first download Nvidia\*.run file from nvidia's website

```sh
sudo dpkg --add-architecture i386
sudo apt update
sudo apt install dkms build-essential libglvnd-dev pkg-config libc6:i386
sudo bash -c "echo blacklist nouveau >> /etc/modprobe.d/blacklist-nouveau.conf"
sudo bash -c "echo options nouveau modeset=0 >> /etc/modprobe.d/blacklist-nouveau.conf"
sudo update-initramfs -u
sudo reboot
sudo telinit 3

# press CTRL + ALT + FX
# then login
# now go to Nvidia\*.run file directory (cd ...)

chmod +x NVIDIA*.run
sudo bash NVIDIA*.run
sudo reboot
```

## Google Chrome

```sh
sudo apt udpate
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
```

## Git

```sh
sudo apt update
sudo add-apt-repository ppa:git-core/ppa
sudo apt install git
```

## Github CLI

```sh
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null

sudo apt update
sudo apt install gh
```

## VLC media player

```sh
sudo apt install vlc
```

## H264 Decoder

```sh
sudo apt update
sudo apt install ubuntu-restricted-extras
# for ubuntu 20.04
sudo apt install libavcodec58 ffmpeg
```

## Visual Studio Code

### Installing using `snap`

```sh
sudo snap install --classic code
```

### Installing using microsoft repository

```sh
sudo add-apt-repository -y "deb [arch=amd64] https://packages.microsoft.com/repos/code stable main"
sudo apt update
sudo apt install code -y
```

## NodeJS

### Installing using a NodeSource PPA

```sh
sudo apt install curl -y
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt update
sudo apt install nodejs
```

### Installing using Node Verson Manager (NVM)

#### Install using scirpt

```sh
# first check the content, use current nvm version
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh
# or
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/0.39.1/install.sh
# after making sure everything is alright, follow the instructions below
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
# to use nvm first source .bashrc
source ~/.bashrc
# list all availble node versions
nvm list-remote
# install choosen version
nvm install <NODE_VERSION>
# check node version
node -v

# use different node versions by installing multiple versions
# and follow the instructions below
nvm use <NODE_VERSION>

```

#### Install usig git

```sh
# go to home directory
cd ~
# clone the repository from github
git clone https://github.com/nvm-sh/nvm.git .nvm
# go into the cloned repository
cd ~/.nvm
# checkout latest version (currently latest: v0.39.1)
git checkout v0.39.1
# activate `nvm` by sourcing it
. ./nvm.sh
```

Now add these lines to your `~/.bashrc` or `~/.zshrc` or `~/.profile`

```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

## MongoDB Community Edition

### Import the public key used by the package management system:

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -

# This operation should respond with an OK.
# if you receive an error indicating that 'gnupg' in not installed, then -
sudo apt-get install gnupg
# once installed, retry importing the key
```

### Create a list file for MongoDB:

```bash
# create the '/etc/apt/sources.list.d/mongodb-org-5.0.list' file
echo "deb [arch=amd64,arm64] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
```

### Install MongoDB packages:

```bash
sudo apt-get update
sudo apt-get install -y mongodb-org
```

### Start MongoDB:

```bash
sudo systemctl start mongod
# if you receive an error - 'Failed to start mongod.service: Unit mongod.service not found' run the following command
sudo systemctl daemon-reload
# then try starting 'mongod' again
```

### Enable MongoDB on startup:

```bash
# check mongodb status
sudo systemctl status mongod
# enable mongodb server on startup
sudo systemctl enable mongod
# disable mongodb server on startup
sudo systemctl disable mongob
# stop mongodb server
sudo systemctl stop mongod
# restart mongodb server
sudo systemctl restart mongod
```

### Use MongoDB Shell

```bash
mongosh
```

### Uninstall MongoDB Community Edition:

```bash
# stop mongod process
sudo systemctl stop mongod
# remove packages
sudo apt-get purge mongodb-org*
# remove data directories
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```

## Docker

Remove previous installations:

```sh
sudo apt remove docker docker.io docker-engine containerd runc
```

### Install using docker repository

#### Setup the repository

1. Update the `apt` package index and install packages to allow `apt` to use a repository over HTTPS:

```sh
sudo apt update
sudo apt install apt-transport-https ca-certificates curl gnupg lsb-release
```

2. Add Docker's official GPG key:

```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

3. Setup the `stable` repository

```sh
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

#### Install Docker Engine

1. Update the `apt` package index, and install the latest version of Docker Engine and containerd

```sh
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
```

2. Verify that Docker Engine is isntalled correctly by running the `hello-world` image

```sh
sudo docker run hello-world
```

### Install from a package

1. Go to `https://download.docker.com/linux/ubuntu/dists/`, choose your ubuntu version, then browse to `pool/stable/`, choose `amd64`, `armhf` or `arm64`, and download the `.deb` file for the Docker Engine version you want to install
2. Navigate to download directory using `cd` and then run the following command -

```sh
sudo dpkg -i package.deb
```

3. Verify that Docker Engine is isntalled correctly by running the `hello-world` image

```sh
sudo docker run hello-world
```

### Install Docker Compose on linux

1. Run this command to download the current stable release of Docker Compose:

```sh
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.6/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

2. Apply executable permissions to the binary:

```sh
sudo chmod +x /usr/local/bin/docker-compose
```

3. Test the installation

```sh
docker-compose --version
```

### Use docker without `sudo` command

1. Run the following commands:

```sh
sudo groupadd docker
sudo usermod -aG docker $USER
```

### Fix `dns` issue in ubuntu

```sh
# check /etc/resolv.conf
cat /etc/resolv.conf
# create a symbolic link to /run/systemd/resolve/resolv.conf
sudo ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf
```

2. Logout and log back in so that your group membership is re-eveluated

## Anaconda

### Anaconda Navigator

Anaconda Navigator is a QT-based GUI, to use this install below packages

```sh
sudo apt install libgl1-mesa-glx libegl1-mesa libxrandr2 libxss1 libxcursor1 libxcomposite1 libasound2 libxi6 libxtst6
```

### Donwload anaconda installation script

```sh
wget -P ~/Downloads/Programs https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh

sha256sum ~/Downloads/Programs/Anaconda3-2020.11-Linux-x86_64.sh

# (optional) check the checksum with the one available at anaconda hashes page
# url: https://docs.anaconda.com/anaconda/install/hashes/Anaconda3-2020.11-x86_64.sh-hash/

# run the script file
bash ~/Downloads/Programs/Anaconda3-2020.11-Linux-x86_64.sh
```

close the current terminal and open again

### Verify conda installation

```sh
conda info
```

> set the auto_activate_base parameter to false

```sh
conda config --set auto_activate_base false
```

> when the script asks, whether you want to run `conda init`, type `yes`

> to initialize conda, type `conda init <shell_name>`

### Open Anaconda Navigator

```sh
anaconda-navigator
```

### Update conda

```sh
conda update --all
```

### Anaconda Environments

```sh
# create environment
conda create --name <environment_name> python=3

# activate environment

conda activate <environment_name>
```

### Uninstall

```sh
rm -rf ~/anaconda3 ~/.conda ~/.condarc ~/.continuum
```

## KVM

### Prerequisites:

- check CPU support for hardware virtualization

```sh
grep -Eoc '(vmx|svm)' /proc/cpuinfo
```

- check if `VT` is enabled in `BIOS` using `kvm-ok` included in `cpu-checker`

```sh
sudo apt update
sudo apt install cpu-checker
kvm-ok
```

### Installing `kvm` on Ubuntu 20.04

```sh
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virtinst virt-manager
```

- `qemu-kvm` - software that provides hardware emulation for the KVM hypervisor
- `libvirt-daemon-system` - configuration files to run the libvirt daemon as a system service
- `libvirt-clients` - software for managing virtualization platforms
- `bridge-utils` - a set of command-line tools for configuring ethernet bridges
- `virtinst` - a set of command-line tools for creating virtual machines
- `virt-manager` - aan easy-to-use GUI interface and supporting command-line utilities for managing virtual machines through libvirt

**Verify libvirt startup:**

```sh
sudo systemctl is-active libvirtd
```

**Add user to `libvirt` and `kvm` groups:**

```sh
sudo usermod -aG libvirt $USER
sudo usermod -aG kvm $USER
```

**List current bridges:**

```sh
brctl show
```

## ZSH Shell

### Installing `zsh` shell:

```sh
sudo apt update
sudo apt install zsh -y
sudo reboot
```

> after reboot, start terminal

### Powerline and Powerline Fonts for `zsh`:

```sh
sudo apt install powerline fonts-powerline -y
```

### `zsh` Powerlevel9k Theme:

```sh
sudo apt install zsh-theme-powerlevel9k -y
# enable theme on startup
echo "source /usr/share/powerlevel9k/powerlevel9k.zsh-theme" >> ~/.zshrc
```

### Powerlevel10 theme:

```sh
git clone git@github.com:romkatv/powerlevel10k ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >> ~/.zshrc
```

now restart terminal

```sh
# if no configuration prompt is shown run,
p10k configure
```

### Set `zsh` as default shell program

```sh
sudo usermod -s $USER
```

## Oh-My-Zsh:

> using `wget`

```sh
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

> using `curl`

```sh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

## Deluge

```sh
sudo apt install deluge
```

## JAVA

### Using repository

```sh
sudo add-apt-repository ppa://webupd8team/java
sudo apt update
sudo apt install oracle-java8-installer
```

### Using snap

```sh
sudo snap install openjdk
```

### Postinstall instructions

add `JAVA_HOME` to .bashrc or .zshrc

```sh
export JAVA_HOME="$(jrunscript -e 'java.lang.System.out.println(java.lang.System.getProperty("java.home"));')"
```

### Change between different `jdks`

```sh
# for java
sudo update-alternatives --config java
# for javac
sudo update-alternatives --config javac
```

or

```sh
update-java-alternatives --list
sudo update-java-alternatives --set /path/to/java/version
```

## Android Studio

### Using repository

```sh
sudo add-apt-repository ppa:maarten-fonville/android-studio
sudo apt update
sudo apt install android-studio
```

### Using snap

```sh
sudo snap install android-studio --classic
```

## Qbittorrent

```sh
sudo add-apt-repository ppa:qbittorrent-team/qbittorrent-stable
sudo apt update
sudo apt install qbittorrent
```

## youtube-dl

```sh
sudo apt install youtube-dl
```

## uGet Download Manager

```sh
sudo add-apt-repository ppa:plushuang-tw/uget-stable
sudo apt update
sudo apt install uget
```

## uGet-integrator

```sh
sudo add-apt-repository ppa:uget-team/ppa
sudo apt update
sudo apt install uget-integrator
```

## XDM - Xtreme Download Manager

```sh
# install
sudo add-apt-repository ppa:noobslab/apps
sudo apt update
sudo apt install xdman

# uninstall
sudo rm /usr/bin/xdman
sudo rm /usr/share/applications/xdman.desktop
sudo rm -r /opt/xdman
```
