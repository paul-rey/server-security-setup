# Fresh Server Security Setup

Based on [serversforhackers.com](https://serversforhackers.com/s/fresh-server-security-setup) setup
and [Initial Secure Server Configuration of Ubuntu 18.04](https://www.vultr.com/docs/initial-secure-server-configuration-of-ubuntu-18-04)

## Secure User Setup

#### Create a new user and setup SSH access on Ubuntu 20.04 Focal.

##### Add new user "someone":
```
sudo adduser someone
```
##### Give user sudo permissions:
```
sudo usermod -aG sudo someone
```
##### switch to your new user
```
su - someone
```
##### Configure your user directory
```
mkdir ~/.ssh
chmod 700 ~/.ssh
```
##### Create authorized_keys file and paste id_ed25519.pub key inside 
```
nano ~/.ssh/authorized_keys
```
```
chmod 600 ~/.ssh/authorized_keys
```
## Secure SSH Setup

#### Configure SSH security on Ubuntu 20.04 Focal.
```
nano /etc/ssh/sshd_config
```

##### Search for 3 values to make sure that OpenSSH is configured properly.

-   `PasswordAuthentication`
-   `PubkeyAuthentication`
-   `ChallengeResponseAuthentication`

##### The values should be set to the following:
```
PasswordAuthentication  no
ChallengeResponseAuthentication  no
PubkeyAuthentication  yes
```

##### Reload sshd with the following command:
```
systemctl reload sshd
```
##### Install fail2ban:

```
sudo apt-get install -y fail2ban
```


Check to make sure a file exists within /etc/fail2ban/jail.d exists with the sshd config similar this:

```
[sshd]
enabled = true
```



## Secure Firewall Setup

#### Setup firewall using ufw

```
sudo ufw allow OpenSSH
```
```
sudo ufw enable
```
