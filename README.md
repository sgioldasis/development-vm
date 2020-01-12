# development-vm

Development VM with Vagrant and Ansible

## Prerequisites

- [VirtualBox 6.0.14](https://www.virtualbox.org/wiki/Download_Old_Builds_6_0)
- [Vagrant](https://www.vagrantup.com/downloads.html)

After you install Vagrant you need to also install some vagrant plugins. Open your terminal and type the following:

```bash
vagrant plugin install vagrant-vbguest
vagrant plugin install vagrant-guest_ansible
```

You can find more info about these plugins in the links below:

https://gist.github.com/tknerr/291b765df23845e56a29
https://github.com/vovimayhem/vagrant-guest_ansible

## Confirm installed software

In your VM open a terminal and type the following:

```bash
# List installed Python versions
pyenv global

# Create Python 3 virtual environment
pyenv virtualenv 3.7.5 dev

# Setup your project to use above virtual environment
cd projects/development-vm/
pyenv local dev 2.7.17

# Check versions of installed software
python --version
pip --version
gcloud --version
docker --version
docker-compose --version
```

Also you will find the following installed software:

- Visual Studio Code
- Chrome

## To do

- No 3d acceleration on first `vagrant up`
