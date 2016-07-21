# CentOS 6.5

### VMWare

### Networking

#### Remote Desktop

<a href="http://ajmatson.net/wordpress/2014/01/install-xrdp-remote-desktop-to-centos-6-5/" target="_blank">Install XRDP Remote Desktop to CentOS 6.5</a>

RHEL/CentOS 6 32-Bit

```
wget http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
rpm -ivh epel-release-6-8.noarch.rpm
```

RHEL/CentOS 6 64-Bit

```
wget http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
rpm -ivh epel-release-6-8.noarch.rpm
```

Install tigervnc

```
yum install xrdp tigervnc-server
service vncserver start
service xrdp start
service iptables stop
chkconfig iptables off
chkconfig xrdp on
chkconfig vncserver on
```

Config control to other users

<code>System</code> &gt; <code>Preferences</code> &gt; <code>Remote Desktop</code>

<img src="http://www.techotopia.com/images/9/93/Centos_6_remote_desktop_preferences.png" alt="" />

#### Firewall

```shell
# start firewall
systemctl start firewalld
# stop firewall
systemctl stop firewalld
# disable firewall
systemctl disable firewalld
# check status
systemctl status firewalld
```

<h4>Development Tools</h4>

Install

```
yum clean all
yum groupinstall &quot;Development tools&quot;
```

<blockquote>
  Warning: CentOS 6 is not support for docker
</blockquote>

#### Static IP

```
## Configure eth0
#
# vi /etc/sysconfig/network-scripts/ifcfg-eth0

DEVICE="eth0"
NM_CONTROLLED="yes"
ONBOOT=yes
HWADDR=A4:BA:DB:37:F1:04
TYPE=Ethernet
BOOTPROTO=static
NAME="System eth0"
UUID=5fb06bd0-0bb0-7ffb-45f1-d6edd65f3e03
IPADDR=192.168.1.44
NETMASK=255.255.255.0


## Configure Default Gateway
#
# vi /etc/sysconfig/network

NETWORKING=yes
HOSTNAME=centos6
GATEWAY=192.168.1.1


## Restart Network Interface
#

/etc/init.d/network restart

## Configure DNS Server
#
# vi /etc/resolv.conf

nameserver 8.8.8.8      # Replace with your nameserver ip
nameserver 192.168.1.1  # Replace with your nameserver ip
```

# CentOS 7

<h4>Remote Desktop <sup id="fnref-1123-1"><a href="#fn-1123-1" rel="footnote">1</a></sup></h4>

```
# add repository rpms
rpm -Uvh https://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-1.el7.nux.noarch.rpm

# install xrdp
yum -y install xrdp tigervnc-server

# start and enable xrdp service
systemctl start xrdp.service
systemctl enable xrdp.service

# add firewall rules
firewall-cmd --permanent --zone=public --add-port=3389/tcp
firewall-cmd --reload

# Configure SELinux
chcon --type=bin_t /usr/sbin/xrdp
chcon --type=bin_t /usr/sbin/xrdp-sesman
```

<h4>Development Tools</h4>

Install

```
yum clean all
yum groupinstall &quot;Development tools&quot;
```

<h4>Install Docker <sup id="fnref-1123-2"><a href="#fn-1123-2" rel="footnote">2</a></sup></h4>

```
# install docker
yum -y update
yum -y install docker docker-registry

# start docker
systemctl enable docker.service
systemctl start docker.service
systemctl status docker.service
```

<div class="footnotes">
<hr />
<ol>

<li id="fn-1123-1">
<a href="http://www.itzgeek.com/how-tos/linux/centos-how-tos/install-xrdp-on-centos-7-rhel-7.html">Install xrdp on CentOS 7 / RHEL 7</a>&#160;<a href="#fnref-1123-1" rev="footnote">&#8617;</a>
</li>

<li id="fn-1123-2">
<a href="http://www.liquidweb.com/kb/how-to-install-docker-on-centos-7/">How To Install Docker on CentOS 7</a>&#160;<a href="#fnref-1123-2" rev="footnote">&#8617;</a>
</li>

</ol>
</div>

### Teamviewer

```
# get teamviewer id
teamviewer --info
```

* You can open teamviewer with normal user in host computer
* You can connect with root user

> **Please Patient when connect to CentOS. HE IS JUST SLOW.**

**Installation**

Step 1: Open Terminal (Applications ——> Utilities ——> Terminal).

Step 2: Switch to root user.

Step 3: Install the prerequisites.

```
# yum install glibc alsa-lib freetype libICE libSM libX11 libXau libXdamage libXext libXfixes libXi libXrandr libXrender libXtst libgcc libuuid libxcb zlib
```

Step 4: Install TeamViewer.

```
# wget http://download.teamviewer.com/download/teamviewer.i686.rpm
# yum install teamviewer.i686.rpm
```

Step 5: Start TeamViewer (Application –> Internet –> TeamViewer)

# Install Pycharm

### Step 1. Open Terminal Window


### Step 2. Download PyCharm for Linux in : [JetBrain](https://www.jetbrains.com/pycharm/download/#section=linux)

### Step 3. From Command Line:

```
tar xvzf pycharm*.tar.gz -C /tmp/
```

### Step 4. Relocating PyCharm
```
sudo su -c "chown -R root:root /tmp/pycharm*"
sudo mv /tmp/pycharm-* /opt/pycharm-*
```

### Step 5. Making PyCharm Symlinks
```
sudo su -c "ln -s /opt/pycharm-community/bin/pycharm.sh /usr/local/bin/pycharm"
sudo su -c "ln -s /opt/pycharm-community/bin/inspect.sh /usr/local/bin/inspect"
```

### Step 6. Launching PyCharm Python IDE
```
pycharm
```
