# Setup VM with K8s Dind Cluster
## 1. Prerequisites Installations (Make sure you have the right version)
### Windows Host
**git** - Just go to http://git-scm.com/download/win and the download will start automatically. Note that this is a project called Git for Windows, which is separate from Git itself; for more information on it, go to https://git-for-windows.github.io/.

**VirtualBox (~5.1)** - https://download.virtualbox.org/virtualbox/5.1.32/VirtualBox-5.1.32-120294-Win.exe 

**Vagrant (~2.0)** - https://releases.hashicorp.com/vagrant/2.0.2/vagrant_2.0.2_x86_64.msi 

### Mac-OS Host
**git** - simply by trying to run git from the Terminal the very first time.`git --version` If you don’t have it installed already, it will prompt you to install it.

**VirtualBox (~5.1)** - https://download.virtualbox.org/virtualbox/5.1.32/VirtualBox-5.1.32-120294-OSX.dmg

**Vagrant (~2.0)** - https://releases.hashicorp.com/vagrant/2.0.2/vagrant_2.0.2_x86_64.dmg

### Linux (Debian-based) Host
**git** - sudo apt-get install  git-all

**VirtualBox (~5.1)** - https://download.virtualbox.org/virtualbox/5.1.32/virtualbox-5.1_5.1.32-120294~Ubuntu~xenial_amd64.deb

**Vagrant (~2.0)** - https://releases.hashicorp.com/vagrant/2.0.2/vagrant_2.0.2_x86_64.deb

## 2. Git clone k8s-training repository
In your host run:
`git clone https://github.com/navivi/k8s-training`

## 3. Vagrant Up
First run: `vagrant plugin install vagrant-disksize`

And then, inside the repository working-dir (cloned in previous step),

run:
`vagrant up`

Make sure you get running VM in your VirtualBox with the name: "k8s_training"

## 4. Change the VM Network Adapter to Bridged
* Shut-Down the VM in Virtualbox
* Right-Click the VM in the VirtualBox and Click 'Settings'
* Choose the 'Network' Tab
* In the 'Attached to' combobox - Choose 'Bridged Adapter' and then click 'OK'
* Start the VM again in Virualbox

## 5. Login to VM Desktop
* Double Click the VM in the VirtualBox (or click 'Show')
* In the console - login with

  > **ubuntu-xenial login:** k8s
  
  > **Password:** Aa123456
  
  > **k8s@ubuntu-xenial:~$** desktop
    
* You should see ubuntu-xenial GUI

## 6. Start K8s Cluster in VM
* In the VM desktop open terminal and run: `./dind-cluster-v1.8.sh up`
* Let it run for few minutes..
* Make sure you get green log: "Access dashboard at:" "http://k8s-training:..."
* Verify you get the k8s dashboard in the VM Browser

# Setup In Ubuntu VM
## Install docker
```bash 
sudo apt-get update
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install docker-ce
sudo usermod -aG docker $USER
```

Need to relogin

### Install kubectl
```bash 
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

echo "source <(kubectl completion bash)" >> ~/.bashrc
```

## Install helm
```bash 
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh
chmod 700 get_helm.sh
./get_helm.sh
```
## Run installation
```bash
./dind-cluster-v1.8.sh up
```
