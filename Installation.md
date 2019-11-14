### Installation

Grafana can be installed on basically any OS like Linux, MAC or Windows.

It even runs in the cloud.

Here we will install it on a fresh CentOS.

You can either install in via the official installer or grab an rpm.

If you choose to add the official repo you need to create the following file

**/etc/yum.repos.d/grafana.repo**

Add the following content.

``` bash
[grafana] 
name=grafana
baseurl=https://packages.grafana.com/oss/rpm
repo_gpgcheck=1 
enabled=1 
gpgcheck=1 
gpgkey=https://packages.grafana.com/gpg.key 
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
```

If you are into beta stuff you can use this repository too.

``` bash
name=grafana
baseurl=https://packages.grafana.com/oss/rpm-beta
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://packages.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
```

Then you need to issue the **yum update** command and then **yum install grafana**

If you just would like to install from the rpm do this.

``` bash
wget https://dl.grafana.com/oss/release/grafana-6.4.4-1.x86_64.rpm
yum localinstall grafana-6.4.4-1.x86_64.rpm
```

Either way you choose there are important things you need to be aware of.

After the installation is done we need to setup the service to automatically start.

``` bash
systemctl enable grafana-server
systemctl start grafana-server
```
