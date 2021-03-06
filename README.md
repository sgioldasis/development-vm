# development-vm

Development VM with Vagrant and Ansible

## Prerequisites

This software has been tested on Linux, OSX and Windows platforms. Before you can use it, you first need to install the following for your specific platform:

- [VirtualBox 6.0.14](https://www.virtualbox.org/wiki/Download_Old_Builds_6_0)
- [Vagrant 2.2.6](https://www.vagrantup.com/downloads.html)

After you install Vagrant you need to also install some vagrant plugins. Open your terminal and type the following:

```bash
vagrant plugin install vagrant-vbguest
vagrant plugin install vagrant-guest_ansible
```

You can find more info about these plugins in the links below:

- <https://github.com/dotless-de/vagrant-vbguest>
- <https://github.com/vovimayhem/vagrant-guest_ansible>
- <https://gist.github.com/tknerr/291b765df23845e56a29>

If you want to clone the repo you need to install [Git](https://git-scm.com/downloads) otherwise you can just download the repo as a ZIP file.

## Usage

Clone (or download) this repo to a local folder on your machine. Open your terminal, `cd` to the above folder and type `vagrant up`. For example if you are using Git you can type the following:

```bash
git clone https://github.com/sgioldasis/development-vm.git
cd development-vm
vagrant up
```

This will create a virtual machine called `dev-vm` in your VirtualBox and install the required software on it. Once the VM has been created, you can change the default machine settings to suit your needs and start the machine from VirtualBox GUI.

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

## Troubleshooting

### Cannot find the given Ansible hosts file

If you get the following error:

```text
ERROR: Cannot find the given Ansible hosts file.
The following SSH command responded with a non-zero exit status.
Vagrant assumes that this means the command failed!

chmod +x /tmp/vagrant-shell && /tmp/vagrant-shell playbook.yml vagrant_ansible_inventory_dev-vm

Stdout from the command:

ERROR: Cannot find the given Ansible hosts file.
```

then you might need to uninstall some other vagrant plugins. To list vagrant plugins installed in your system you can type:

```bash
vagrant plugin list
```

Ideally, you should get this output:

```bash
vagrant-guest_ansible (0.0.4, global)
vagrant-vbguest (0.23.0, global)
```

Plugin `vagrant-hostmanager` has been known to cause the issue. You can uninstall it by running the following:

```bash
vagrant plugin uninstall vagrant-hostmanager
```
