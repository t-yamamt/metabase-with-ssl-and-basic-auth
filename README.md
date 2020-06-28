# Easy deployment of Metabase with a Nginx reverse proxy for SSL and basic auth

## Usage

### Prerequisite: install docker and docker-compose

An example for RHEL/CentOS 7 as follows:
```ShellSession
update installed packages
$ sudo yum update -y

confirm timezone
$ timedatectl
set timezone you want
$ sudo su root
# timedatectl set-timezone Asia/Tokyo
# exit

install yum util
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2

add docker-ce repo
$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

install docker-ce
$ sudo yum install -y docker-ce docker-ce-cli containerd.io

start docker
$ sudo systemctl start docker

confirm docker has started
$ sudo docker --version

configure docker service to start up automatically when rebooting
$ sudo systemctl enbale docker

install docker-compose
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose
$ sudo chmod +x /usr/bin/docker-compose

confirm docker-compose command has installed
$ sudo docker-compose --version
```

### 1. Clone this repo

You clone this repo in anywhere you want. In the below, I use `/opt` for example.

```ShellSession
$ cd /opt
$ git clone https://github.com/t-yamamt/metabase-with-ssl-and-basic-auth.git
```

### 2. Modify environment variables for containers

You must modify .env after your enviroment and what you want.
Remember, if you modify `MB_DB_HOST`, you should also modify service name of MySQL in docker-compose.yml.

### 3. Configure your domain

Based on .env settings, you must configure your domain with DNS adding an A record for your domain and your static IP address.

### 4. Create containers

Finally, you can create containers. Remember you have to wait for configuring Let's Encrypt in Nginx container (https-portal) for a bit long time.

```ShellSession
$ cd /opt/metabase-with-ssl-and-basic-auth
$ sudo docker-compose up -d
```

If you don't need containers anymore, you can remove them like the below:

```ShellSession
$ sudo docker-compose rm -fs
```


