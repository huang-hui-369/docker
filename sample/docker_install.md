# docker install

## 1. Uninstall old versions
```
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

## 2. install yum-utils plugin and set stable repository

```
# install yum-utils plugin
sudo yum install -y yum-utils

# set stable repository
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

```

## 3. install the latest docker engine
```
# install the latest docker engine
$ sudo yum install docker-ce docker-ce-cli containerd.io
```
Docker is installed but not started. The docker group is created, but no users are added to the group.

## 4. sudo Start Docker
   `$ sudo systemctl start docker`

## 5. create user futari
   ```
   useradd futari
   passwd futari
   ```
## 6. user futari add to group docker
   `$ sudo usermod -aG docker futari`

## 7. change to user futari
   `su futari`

## 8. Verify that Docker Engine is installed correctly 
   `$ docker run hello-world`