# zabbix-agent-on-RasPi

Install Zabbix

Install and configure Zabbix for your platform

a. Install Zabbix repository
Documentation
```
wget https://repo.zabbix.com/zabbix/7.0/raspbian/pool/main/z/zabbix-release/zabbix-release_latest_7.0+debian12_all.deb
sudo dpkg -i zabbix-release_latest_7.0+debian12_all.deb
sudo apt update
```
b. Install Zabbix agent 2
Install zabbix-agent2 package.
```
sudo apt install zabbix-agent2
```
c. Install Zabbix agent 2 plugins
Documentation
You may want to install Zabbix agent 2 plugins.
```
sudo apt install zabbix-agent2-plugin-mongodb zabbix-agent2-plugin-mssql zabbix-agent2-plugin-postgresql
```

d. edit Zabbgix agent config
```
sudo nano /etc/zabbix/
```

e. Start Zabbix agent 2 process
Start Zabbix agent 2 process and make it start at system boot.
```
sudo systemctl restart zabbix-agent2
sudo systemctl enable zabbix-agent2
```


Script and template for zabbix-agent to run on raspberryPi.
I assume you already installed zabbix-agent
`sudo apt install zabbix-agent`

Fetch script from GitHub:
```
wget https://raw.githubusercontent.com/thuer-it/zabbix-agent-on-RasPi/master/raspberrypi.sh
```

Create script location:
```
sudo mkdir /etc/zabbix/scripts
```

Move script to new location:
```
sudo mv raspberrypi.sh /etc/zabbix/scripts
```

Change permissions for script:
```
sudo chmod 755 /etc/zabbix/scripts/raspberrypi.sh
```

Add zabbix user to video group to get required permissions.
```
sudo usermod -aG video zabbix
```

Test script:
```
$ /etc/zabbix/scripts/raspberrypi.sh temperature
50464
```

Add script to zabbix configuration file:
```
sudo nano /etc/zabbix/zabbix_agentd.conf
```

Adding the following line:
```
UserParameter=raspberrypi.sh[*],/etc/zabbix/scripts/raspberrypi.sh $1
```

Restart the zabbix agent:
```
sudo service zabbix-agent restart
```

Import the Template in your Zabbix Server frontend.
Assign it to the host.

# Thanks to 
Bernhard Linz for his Tutorial and Script on [http://znil.net/index.php/Zabbix:Template_Raspberry_Pi]
