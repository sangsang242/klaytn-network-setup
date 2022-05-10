# Klaytn Network Setup
 To build klaytn core cell network locally via docker-compose for learning purpose

## Requirements
Environment with docker & docker-compose installed

- Install docker and docker-compose manually or
- Use docker installed AMI

Check out docker and docker-compose installation
```
$ docker ps -a
$ docker-compose --version
```


```
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
```

## Preparation

Start cloning repository
```
$ git clone https://github.com/sangsang242/klaytn-network-setup.git
```

Install RPM packages in the repository directory
```
$ cd klaytn-network-setup

$ wget https://packages.klaytn.net/klaytn/v1.7.3/homi-v1.7.3-0.el7.x86_64.rpm
$ wget https://packages.klaytn.net/klaytn/v1.7.3/kcnd-v1.7.3-0.el7.x86_64.rpm
$ wget https://packages.klaytn.net/klaytn/v1.7.3/kpnd-v1.7.3-0.el7.x86_64.rpm
$ wget https://packages.klaytn.net/klaytn/v1.7.3/kend-v1.7.3-0.el7.x86_64.rpm
```

Start servers via docker compose
```
$ docker-compose --file klaytn-compose.yaml up -d 
```

## Installation
### Network default value generation
**Note** `docker exec -it {{container name specified in yaml}} bash`
```
$ docker exec -it cn-1 bash

# cd /tmp
# rpm -ivh homi-v1.7.3-0.el7.x86_64.rpm
# homi setup ...
# vi /usr/share/homi-output/scripts/static-nodes.json
"kni://...@0.0.0.0:32323 -> "kni://...@cn-1:32323
"kni://...@0.0.0.0:32324 -> "kni://...@cn-2:32323
...
```

### Consensus Node
```
$ docker exec -it cn-# bash

# rpm -ivh /tmp/kcnd-v1.7.3-0.el7.x86_64.rpm
...
```

## Useful commands
### Check out klaytn data
At host
```
$ sudo ls -alh /var/lib/docker/volumes/{{repository-name}}_{{volume-name}}/_data/klaytn
```

### Deleting docker containers and volumes
```
$ docker-compose --file klaytn-compose.yaml down

$ docker system prune -a -f --volumes
```
