# TFE interactive online installation using Vagrant

## Intro

This manual is dedicated for Terraform Enterprise online interactive installation using Vagrant.

Tested on Mac OS X.

## Requirements

- Oracle Virtualbox recent version installed
[VirtualBox installation manual](https://www.virtualbox.org/manual/ch01.html#intro-installing)

- Hashicorp vagrant recent version installed
[Vagrant installation manual](https://learn.hashicorp.com/tutorials/vagrant/getting-started-install)

- git installed
[Git installation manual](https://git-scm.com/download/mac)

## Preparation 

- Clone git repository. 

```bash
git clone https://github.com/antonakv/tfe-vagrant-online-pmd
```

Expected command output looks like this:

```bash
Cloning into 'tfe-vagrant-online-pmd'...
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (12/12), done.
remote: Compressing objects: 100% (12/12), done.
remote: Total 12 (delta 1), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (12/12), done.
Resolving deltas: 100% (1/1), done.
```

- Change folder to tfe-vagrant-online-pmd

```bash
cd tfe-vagrant-online-pmd
```

- Copy your existing Terraform enterprise license file with extension .rli to 
folder tfe-vagrant-online-pmd created on the previous step and rename it to license.rli

## Installation

- In the same folder you were before run: 

```bash
vagrant up
```

Sample result

```bash
$ vagrant up     
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'aakulov/bionic64'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'aakulov/bionic64' version '21.03.02' is up to date...
==> default: A newer version of the box 'aakulov/bionic64' for provider 'virtualbox' is
==> default: available! You currently have version '21.03.02'. The latest is version
==> default: '21.05.27'. Run `vagrant box update` to update.
==> default: Setting the name of the VM: tfe-vagrant-online-pmd_default_1622103422132_97669
==> default: Fixed port collision for 22 => 2222. Now on port 2200.
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
    default: Adapter 2: hostonly
==> default: Forwarding ports...
    default: 22 (guest) => 2200 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2200
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: 
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default: 
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Setting hostname...
==> default: Configuring and enabling network interfaces...
==> default: Mounting shared folders...
    default: /vagrant => /Users/aakulov/Documents/Development/Hashicorp/tfe-vagrant-online-pmd

```

- Connect to provisioned VM using

```bash
vagrant ssh
```

Sample output

```bash 
$ vagrant ssh
Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 4.15.0-136-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
New release '20.04.2 LTS' available.
Run 'do-release-upgrade' to upgrade to it.

```

- Run the TFE installer

```bash
curl https://install.terraform.io/ptfe/stable | sudo bash
```

Sample output

```bash
$ curl https://install.terraform.io/ptfe/stable | sudo bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  145k  100  145k    0     0  15427      0  0:00:09  0:00:09 --:--:-- 36091
Determining local address
The installer was unable to automatically detect the private IP address of this machine.
Please choose one of the following network interfaces:
[0] enp0s3	10.0.2.15
[1] enp0s8	192.168.56.33
Enter desired number (0-1): 

```

- Enter number which corresponds IP address 192.168.56.33. It's 1 in the current example.

```bash
1
```

Sample output

```bash
Enter desired number (0-1): 1
The installer will use network interface 'enp0s8' (with IP address '192.168.56.33').
Determining service address
The installer was unable to automatically detect the service IP address of this machine.
Please enter the address or leave blank for unspecified.
Service IP address: 
```

- Push "Enter" key

Sample output

```bash
The installer was unable to automatically detect the service IP address of this machine.
Please enter the address or leave blank for unspecified.
Service IP address: 
Does this machine require a proxy to access the Internet? (y/N) 
```

- Push "N" key

Sample output

```bash
Does this machine require a proxy to access the Internet? (y/N) n
Installing docker version 19.03.8 from https://get.replicated.com/docker-install.sh
# Executing docker install script, commit: b50fac9
+ sh -c apt-get update -qq >/dev/null
+ sh -c DEBIAN_FRONTEND=noninteractive apt-get install -y -qq apt-transport-https ca-certificates curl >/dev/null
+ sh -c curl -fsSL "https://download.docker.com/linux/ubuntu/gpg" | apt-key add -qq - >/dev/null
Warning: apt-key output should not be parsed (stdout is not a terminal)
+ sh -c echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" > /etc/apt/sources.list.d/docker.list
+ sh -c apt-get update -qq >/dev/null
INFO: Searching repository for VERSION '19.03.8'
INFO: apt-cache madison 'docker-ce' | grep '19.03.8.*-0~ubuntu' | head -1 | awk '{$1=$1};1' | cut -d' ' -f 3
+ [ -n 5:19.03.8~3-0~ubuntu-bionic ]
+ sh -c apt-get install -y -qq --no-install-recommends docker-ce-cli=5:19.03.8~3-0~ubuntu-bionic >/dev/null
+ sh -c apt-get install -y -qq --no-install-recommends docker-ce=5:19.03.8~3-0~ubuntu-bionic >/dev/null
+ sh -c docker version
Client: Docker Engine - Community
 Version:           19.03.8
 API version:       1.40
 Go version:        go1.12.17
 Git commit:        afacb8b7f0
 Built:             Wed Mar 11 01:25:46 2020
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.8
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.12.17
  Git commit:       afacb8b7f0
  Built:            Wed Mar 11 01:24:19 2020
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.4
  GitCommit:        05f951a3781f4f2c1911b05e61c160e9c30eaa8e
 runc:
  Version:          1.0.0-rc93
  GitCommit:        12644e614e25b05da6fd08a38ffa0cfe1903fdec
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
If you would like to use Docker as a non-root user, you should now consider
adding your user to the "docker" group with something like:

  sudo usermod -aG docker your-user

Remember that you will have to log out and back in for this to take effect!

WARNING: Adding a user to the "docker" group will grant the ability to run
         containers which can be used to obtain root privileges on the
         docker host.
         Refer to https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface
         for more information.
External script is finished
Synchronizing state of docker.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable docker

Running preflight checks...
[INFO] / disk usage is at 14%
[INFO] /var/lib/docker disk usage is at 1%
[INFO] Docker http proxy not set
[INFO] Docker using default seccomp profile
[INFO] Docker using standard root directory
[INFO] Docker icc (inter-container communication) enabled
[INFO] Docker open files (nofile) ulimit not set
[INFO] Docker userland proxy enabled
[INFO] Firewalld is not active
[INFO] Iptables chain INPUT default policy ACCEPT
Pulling replicated and replicated-ui images
stable-2.52.0: Pulling from replicated/replicated
Image docker.io/replicated/replicated:stable-2.52.0 uses outdated schema1 manifest format. Please upgrade to a schema2 image for better future compatibility. More information at https://docs.docker.com/registry/spec/deprecated-schema-v1/
69692152171a: Pull complete 
4cec2ee532ca: Pull complete 
5e5336345ecc: Pull complete 
8c9af647b5fd: Pull complete 
f29b1c17ff51: Pull complete 
fce3e81d9123: Pull complete 
d94558f8f63a: Pull complete 
657e54daabf4: Pull complete 
dfa55743770a: Pull complete 
82a73fe0e9b9: Pull complete 
9c9b8421b4c8: Pull complete 
Digest: sha256:d38833cb625b0e226471f59f8a894469e76c44035288d9a57560bb8620b114b4
Status: Downloaded newer image for replicated/replicated:stable-2.52.0
docker.io/replicated/replicated:stable-2.52.0
stable-2.52.0: Pulling from replicated/replicated-ui
Image docker.io/replicated/replicated-ui:stable-2.52.0 uses outdated schema1 manifest format. Please upgrade to a schema2 image for better future compatibility. More information at https://docs.docker.com/registry/spec/deprecated-schema-v1/
69692152171a: Already exists 
d26ac9469008: Pull complete 
92d885dd2446: Pull complete 
0a0630b58335: Pull complete 
8db0096a6f1e: Pull complete 
95d2036e9098: Pull complete 
Digest: sha256:7c5a916b9e265fa23677b797d278c44ac9bab3ba6f402927cc1fa6a43e5d6348
Status: Downloaded newer image for replicated/replicated-ui:stable-2.52.0
docker.io/replicated/replicated-ui:stable-2.52.0
Tagging replicated and replicated-ui images
Stopping replicated and replicated-ui service
Installing replicated and replicated-ui service
Starting replicated and replicated-ui service
Created symlink /etc/systemd/system/docker.service.wants/replicated.service → /etc/systemd/system/replicated.service.
Created symlink /etc/systemd/system/docker.service.wants/replicated-ui.service → /etc/systemd/system/replicated-ui.service.
Installing replicated command alias
Installing local operator
Installing local operator with command:
curl -sSL https://get.replicated.com/operator?replicated_operator_tag=2.52.0
Pulling latest replicated-operator image
stable-2.52.0: Pulling from replicated/replicated-operator
Image docker.io/replicated/replicated-operator:stable-2.52.0 uses outdated schema1 manifest format. Please upgrade to a schema2 image for better future compatibility. More information at https://docs.docker.com/registry/spec/deprecated-schema-v1/
69692152171a: Already exists 
b8d1591cc3e8: Pull complete 
99408039ae2c: Pull complete 
f9266063add8: Pull complete 
3669a4e3d61c: Pull complete 
69bf04578910: Pull complete 
bc03da138eb1: Pull complete 
Digest: sha256:bd80d36e0a6dfe0ef8a50e858db9680418a072cd53f084caf4b488a294d8fcb9
Status: Downloaded newer image for replicated/replicated-operator:stable-2.52.0
docker.io/replicated/replicated-operator:stable-2.52.0
Tagging replicated-operator image
Stopping replicated-operator service
Installing replicated-operator service
Starting replicated-operator service
Created symlink /etc/systemd/system/docker.service.wants/replicated-operator.service → /etc/systemd/system/replicated-operator.service.

Operator installation successful

To continue the installation, visit the following URL in your browser:

  http://<this_server_address>:8800
```

- In your browser open URL https://192.168.56.33:8800/

![Initial screen](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-1.png)

- Click Advanced - Proceed to 192.168.56.33 (unsafe)

![Proceed](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-2.png)

Expected result

![Expected result](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-3.png)

- Enter `192.168.56.33.nip.io` to Hostname field and click `Use Self-Signed Cert`

![Self signed](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-4.png)

- In your browser open URL https://192.168.56.33.nip.io:8800/

![Upload certificate](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-5.png)

- Click `Choose license` and select your TFE license file. Then click `Open`

![Upload license](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-6.png)

- Click `Online`

![Online](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-7.png)

- Click `Continue`

![Continue](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-8.png)

- Enter password `Password1#` to Password and Confirm password fields. Click `Continue`

![Password](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-9.png)

- On the next screen scroll down and click `Continue`

![Proceed anyway](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-10.png)

- On the Settings page set `Encryption password` as `Password1#` and select installation type `Production`. 

![Encryption password](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-12.png)

- Select Production type `Mounted disk` and fill `Path on Host` with `/mnt/disk`

![Mounted disk](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-17.png)

- Go to the end of the page and click `Save`

![Save](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-13.png)

- Click `Restart now`

![Restart now](https://github.com/antonakv/tfe-vagrant-online-pmd/raw/main/images/tfe-i-vagrant-14.png)

## Usage

Tested in Google Chrome

- In your browser open URL https://192.168.56.33.xip.io:8800/

- Enter password ```Password1#``` and click ```Unlock```

 ![Unlock](https://github.com/antonakv/tfe-vagrant/raw/main/images/tfe-vagrant-2.png)

- Open URL https://192.168.56.33.xip.io:8800/dashboard

  ![Dashboard](https://github.com/antonakv/tfe-vagrant/raw/main/images/tfe-vagrant-7.png)

