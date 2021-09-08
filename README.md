# ansible-playbooks
Wonna be Ansible playbook for setting up dev-vm. Currently its just a list of commands and instructions to setup my VM.

# setup my dev VM
Note: replace `{user}` with the new user name in the VM.

## install qemu-guest-agent
sudo apt-get update\
sudo apt-get install qemu-guest-agent\
sudo systemctl enable qemu-guest-agent

## user setup steps
useradd -m {user}\
passwd {user}

## firewall setup
sudo ufw enable\
sudo ufw allow 22\
sudo ufw allow 2222

## ssh setup
/etc/ssh/sshd_config Port 2222 \
/etc/ssh/sshd_config PasswordAuthentication no \
sudo service ssh restart \
ssh-copy-id ioannis@ioannis-vm

## install docker
sudo apt-get update
```
sudo apt-get install \
      apt-transport-https \
      ca-certificates \
      curl \
      gnupg \
      lsb-release
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg \
```
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
sudo apt-get update \
sudo apt-get install docker-ce docker-ce-cli containerd.io

## install docker-compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
sudo chmod +x /usr/local/bin/docker-compose

## create ssh key
ssh-keygen -t rsa -b 4096 -C "name@domain.com"

## create code directory
mkdir ~/code && ~/code \
git clone ...

## add user to docker group
sudo usermod -aG docker {user}

## setup psql
sudo apt install postgresql-client-common

## setup golang
sudo snap install go --classic

## setup vim
scp -P 2222 ~/.vimrc {user}@{user}-dev-vm:~/.vimr

# manually install plugins
run :GoInstallBinaries to setup vim-go plug-in

## setup python
sudo apt install python3-pip \
python3 -m pip install pre-commit

## tools
sudo apt install net-tools \
sudo apt install ipmiutil \
go install https://github.com/nektos/act \
sudo apt install jq \
curl -L https://github.com/hasura/graphql-engine/raw/stable/cli/get.sh | bash \
sudo apt install moreutils
