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
 ---

### To Install IPTables on Fedora

1.
**disable firewalld using the systemctl command.**

`sudo systemctl stop firewalld`

`sudo systemctl disable firewalld`

`systemctl mask firewalld`

### Install IPTables
`sudo dnf install iptables-services`

**Enable IPTables**

systemctl start iptables.service

systemctl enable iptables.service

**Configure IPTables file**
`/etc/sysconfig/iptables`

**IPTables Lists**
`iptables -L`

**Stop and Disable IPTables**
`sudo systemctl stop iptables`
`sudo systemctl disable iptables`

**Restart IPTables**
`sudo systemctl restart iptables`

### Install Golang
```
sudo dnf install golang
mkdir -p $HOME/go
echo 'export GOPATH=$HOME/go' >> $HOME/.bashrc
source $HOME/.bashrc

```
Check that GOPATH is set correctly with this command:

```
go env GOPATH
/home/user/go
```
### Install an RPM File On Linux OS CentOS, RHEL, & Fedora

```
sudo yum install wget
sudo dnf install wget
wget http://<website>/sample_file.rpm
sudo rpm -i <file>.rpm

$ Install on Fedora
sudo rpm -i <file>.rpm
sudo dnf localinstall <file>.rpm

$ Remove Rpm package
sudo rpm -e <file>.rpm
    -q – This option tells RPM to query the file
    -p – This option lets you specify the target package to query
    -R – This lists the requirements for the package

$ Download RPM Packages from the Repository
sudo yumdownloader packagename
    
```

---

**Install nasm on fedora **
`sudo dnf install nasm`

