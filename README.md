# Nixes
Welcome to the Nixes wiki!

### Install VirtualBox on Fedora

`$ sudo dnf -y install @development-tools`
`$ sudo dnf -y install kernel-headers kernel-devel dkms elfutils-libelf-devel qt5-qtx11extras`

**add the VirtualBox RPM repository.**

`$ cat <<EOF | sudo tee /etc/yum.repos.d/virtualbox.repo `
`[virtualbox]`
`name=Fedora $releasever - $basearch - VirtualBox`
`baseurl=http://download.virtualbox.org/virtualbox/rpm/fedora/36/\$basearch`
`enabled=1`
`gpgcheck=1`
`repo_gpgcheck=1`
`gpgkey=https://www.virtualbox.org/download/oracle_vbox.asc`
`EOF`

**import the VirtualBox GPG key.**

`$ sudo dnf search virtualbox`


**install VirtualBox.**

`$ sudo dnf install VirtualBox-7.0`

**execute the following command in terminal to open the program.**

`$ virtualbox`

