Welcome to the Nixes wiki!

### Install VirtualBox on Fedora

```C
$ sudo dnf -y install @development-tools
$ sudo dnf -y install kernel-headers kernel-devel dkms elfutils-libelf-devel qt5-qtx11extras

```

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

# or 

### Step 1. First, install the required dependencies:

`$ sudo dnf -y install @development-tools`
`$ sudo dnf -y install kernel-headers kernel-devel dkms elfutils-libelf-devel qt5-qtx11extras`

### Step 2. Next, we will add the VirtualBox package repository by downloading it from virtualbox.org:

`$ sudo wget -P /etc/yum.repos.d/ https://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo`

### Step 3. Import the VirtualBox GPG key:

`$ sudo dnf search virtualbox`

Answer Y when asked for confirmation.

### Step 4. Finally, install the latest version of VirtualBox:

`$ sudo dnf install VirtualBox <--version -->`

### Step 5. Add your user to the vboxusers group to enable USB usage:

`$ sudo usermod -aG vboxusers $USER`


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

**Install nasm on fedora**
`sudo dnf install nasm`

---

### Install MySQL 8.0 on Fedora


**1: Add MySQL 8.0 community repository**
To install MySQL 8.0 on Fedora, you need to add MySQL 8.0 community repository.
`sudo dnf -y install https://dev.mysql.com/get/mysql80-community-release-fc38-1.noarch.rpm`
This will write a repository file to `/etc/yum.repos.d/mysql-community.repo`
` cat /etc/yum.repos.d/mysql-community.repo`


---

**2: Install MySQL Server 8.0 on Fedora**
Once you have added the repository and confirm to be enabled, proceed to install MySQL 8.0 onto your Fedora by running:
`sudo dnf install mysql-community-server`
After installation, the package info can be seen from:
`rpm -qi mysql-community-server`

---

**3: Configure MySQL server on Fedora**
After installation of MySQL 8.0 on Fedora, you need to do initial configuration to secure it.

1. Start and enable mysqld service:
```sql
sudo systemctl start mysqld.service
sudo systemctl enable mysqld.service
```
2. Copy the generated random password for the root user
`sudo grep 'A temporary password' /var/log/mysqld.log |tail -1`
Take note the printed password:

`A temporary password is generated for root@localhost: 1ph/axo>vJe;`
3. Start MySQL Secure Installation to change the root password, Disallow root login remotely, remove anonymous users and remove test database.

```sql
`$ sudo mysql_secure_installation`
Securing the MySQL server deployment.
Enter password for user root:
```
Authenticate with your generated temporary password. Then configure your MySQL 8.0 installation like below:

```sql
Change the password for root ? ((Press y|Y for Yes, any other key for No) : Yes

New password: 
Re-enter new password: 

Estimated strength of the password: 100 
Do you wish to continue with the password provided?: Yes

Remove anonymous users?: Yes
Success.

Disallow root login remotely? : Yes
Success.

Remove test database and access to it? : Yes
 - Dropping test database...
Success.
 - Removing privileges on test database...
Success.

Reload privilege tables now? (Press y|Y for Yes) : Yes
Success.

All done!

```
4. Connect to MySQL Database as root user and create a test database.

```sql
$ sudo mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 8.0.33

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> SELECT version();
+-----------+
| version() |
+-----------+
| 8.0.33    |
+-----------+
1 row in set (0.00 sec)
```

```sql
Create a test database and user

mysql> CREATE DATABASE test_db;
Query OK, 1 row affected (0.09 sec)

mysql> CREATE USER 'test_user'@'localhost' IDENTIFIED BY "Strong34S;#";
Query OK, 0 rows affected (0.04 sec)

mysql> GRANT ALL PRIVILEGES ON test_db.* TO 'test_user'@'localhost';
Query OK, 0 rows affected (0.02 sec)

mysql> FLUSH PRIVILEGES;

Query OK, 0 rows affected (0.02 sec)
This test database and user can be dropped by running:

mysql> DROP DATABASE test_db;
Query OK, 0 rows affected (0.14 sec)

mysql> DROP USER 'test_user'@'localhost';
Query OK, 0 rows affected (0.11 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.01 sec)

mysql> QUIT
Bye

```
**4: Configure Firewall for remote connections**
To allow for remote connections, allow port 3306 on the firewall

```sql
sudo firewall-cmd --add-service=mysql --permanent
sudo firewall-cmd --reload
You can also limit access from trusted networks

sudo firewall-cmd --permanent --add-rich-rule 'rule family="ipv4" \
service name="mysql" source address="10.1.1.0/24" accept'

```

---

### Configure DNF for a Quicker Mirror Updates and Repos Installations Fedora


```C
sudo nano /etc/dnf/dnf.conf   see `man dnf.conf` for defaults and possible options

[main]
gpgcheck=1
installonly_limit=3
clean_requirements_on_remove=True
best=False
skip_if_unavailable=True


```

A configuration file for DNF (Dandified Yum), a package manager used in some Linux distributions such as Fedora. Let me break down the configuration settings you have in this file:

`gpgcheck=1:`
 This setting enables GPG signature checking for packages. It ensures that packages are signed by the specified key before they are installed.

`installonly_limit=3:`
This setting limits the number of versions of a package that can be installed simultaneously. In this case, it's set to 3, meaning that only the three most recent versions of a package will be kept.

`clean_requirements_on_remove=True:`
When a package is removed, this setting ensures that any dependencies that were installed only for that package and are no longer needed by other packages are also removed.

`best=False:`
This setting, when set to False, prevents DNF from automatically upgrading to the latest version of a package if a newer version is available. If set to True, DNF will try to upgrade to the latest version.

`skip_if_unavailable=True:`
If a repository is unavailable or encountering errors, this setting instructs DNF to skip it and proceed with other available repositories. If set to False, DNF would fail if any repository is unreachable.

This configuration file allows you to customize the behavior of DNF according to your preferences and requirements.

---

### Connect Web-Cam on Fedora
```HTML
sudo fuser -v /dev/video*
sudo lsmod | grep uvcvideo
sudo dnf install v4l-utils
v4l2-ctl --list-devices
sudo dnf install guvcview
```

---

### Install Weka on Fedora

```Bash
sudo ln -s /var/lib/snapd/snap /snap

sudo snap install weka

```
---

### Installing and running Fedora Media Writer On Fedora

On Fedora 25 or later, Fedora Media Writer is available in the default repository. You can use dnf to install the package.

    To install the Fedora Media Writer using:

    `sudo dnf install mediawriter`

    Run the Fedora Media Writer:

   ` mediawriter`

---

### How to fix WirePlumber high CPU usage

 1.Enable [monosoul/wireplumber-high-cpu-usage-fix](https://copr.fedorainfracloud.org/coprs/monosoul/wireplumber-high-cpu-usage-fix/) COPR
```
sudo dnf copr enable monosoul/wireplumber-high-cpu-usage-fix`

```

2. Update repo metadata and install the new WirePlumber package
```
sudo dnf update --refresh

```
3. Restart WirePlumber
```
systemctl --user restart wireplumber

```

---

## Cuda Installation and Configuration

### Install local repository on file system:

`sudo rpm --install cuda-repo-<distro>-X-Y-local-<version>*.x86_64.rpm`

### Install the new CUDA public GPG key:
`sudo dnf config-manager --add-repo https://developer.download.nvidia.com/compute/cuda/repos/$distro/x86_64/cuda-$distro.repo`

### Clean DNF repository cache:

`sudo dnf clean expire-cache`

### Install CUDA SDK:

`sudo dnf module install nvidia-driver:latest-dkms`
`sudo dnf install cuda-toolkit`

`sudo dnf --disablerepo="rpmfusion-nonfree*" install cuda`
`sudo grub2-mkconfig -o /boot/grub2/grub.cfg`

### Reboot the system:

`sudo reboot`

### Check Version
`nvcc --version`

---
## Set up VMware player on Fedora

```yumi

   0 sudo dnf install kernel-devel
    
   1  sudo VMware-Player-Full-17.5.1-23298084.x86_64.bundle
   2  chmod +x VMware-Player-Full-17.5.1-23298084.x86_64.bundle
   3  sudo ./VMware-Player-Full-17.5.1-23298084.x86_64.bundle

```
---
### Installation of flatpak and WPS office on Fedora!

```html
sudo flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
x1869@fedora:~$ flatpak install flathub com.wps.Office -y
flatpak remote-modify --enable flathub
```

---

### Install zsh on Ubuntu

```Bash
Before installing z shell, you must first update your system by running the following command:

sudo apt update
After successfully updating your system, run the following command to install zshell.

sudo apt install zsh

sudo apt install zsh-syntax-highlighting zsh-autosuggestions

sudo apt install qterminal fonts-firacode gnome-tweaks

chsh -s /bin/zsh

rm ~/.zshrc

touch ~/.zshrc

source .zshrc


```
---

```css

 ### Wireshark can output dissected packets as .csv file.

1. Open .pcap file with Wireshark.
2. Filter packets you want to export.
3. Go to File->Packet Dissections->As CSV ...
4. Select Displayed in Packet Range if you want to export only filtered packets.
5. Save your file.

```
### Install XAMPP on Linux:

**Download the XAMPP installer package:**
Visit [https://www.apachefriends.org/download.html](https://www.apachefriends.org/download.html?ref=hackernoon.com)) to download the appropriate installer for your Linux distribution.

**Change file permissions:**
Open the terminal and navigate to the directory containing the downloaded package.
Execute the command `sudo chmod +x xampp-linux-*-installer.run` to make the installer executable.

**Run the XAMPP installer:**
Run the installer using the command `sudo ./xampp-linux-*-installer.run.`

**Follow the installation wizard:**
The wizard will guide you through language selection, installation location, and component choices.

**Start the XAMPP server:**
After installation, start the server with `sudo /opt/lampp/lampp.`

**Verify the installation:**
Open a web browser and go to `http://localhost` to confirm the successful installation by viewing the XAMPP welcome page.

### Linux:

Open a terminal window.
Navigate to the XAMPP installation directory (e.g., `/opt/lampp`).
Run the following command:
`sudo /opt/lampp/lampp start`
Verify that the XAMPP server is running by opening a web browser and navigating to `http://localhost.`
Once the XAMPP server is started, you can access it by navigating to `http://localhost` in your web browser. You can also access specific XAMPP components by navigating to the following URLs:

* **Apache**:` http://localhost/xampp/`
* **PHPMyAdmin:** `http://localhost/phpmyadmin/`
* **MariaDB:**`http://localhost:3306/`
* **FTP Server:** `ftp://localhost/`

