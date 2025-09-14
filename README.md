# hello_world
This is an example of Hello World website powered by nginx inside a Docker container.

# 1- How to setup Docker
First we need to ensure that Docker is installed and working. Installation depends on the OS you are running.

## For Debian/Ubuntu based Distros
1- Set up Docker's apt repository.
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
2- Install Docker 
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
3- Make sure Docker is installed
```
sudo docker --version
```
If the outpus is like this, it means that Docker installation is done
```
Docker version 28.3.3, build 1.fc42
```
## For RHEL based Distros
1- Set up Docker dnf repository
```
sudo dnf -y install dnf-plugins-core
 sudo dnf-3 config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
```
2-Install Docker packages
```
 sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
3-Enable the Docker engine through systemctl, with this command, Docker will boot automatically everytime we boot the system
```
sudo systemctl enable --now docker
```
If the outpus is like this, it means that Docker installation is done
```
Docker version 28.3.3, build 1.fc42
```

---
## Running the Container

You can add your user to docker group to grant permissions, otherwise you will need to use sudo at the beginning for docker commands
```
sudo groupadd docker        
sudo usermod -aG docker $USER 
```
Log out to apply the changes

---

First we need to pull the hello_world image from the docker hub.
```
docker pull bkarabacak/hello_world:latest
```

To see all the images you pulled,
```
docker images
```
You will see all the images are installed on the device 
```
REPOSITORY                      TAG       IMAGE ID       CREATED         SIZE
alpine                          latest    91ef0af61f39   12 months ago   7.79MB
nginx                           alpine    c7b4f26a7d93   13 months ago   43.2MB
nginx                           latest    39286ab8a5e1   13 months ago   188MB
postgres                        latest    b781f3a53e61   13 months ago   432MB
ubuntu                          latest    edbfe74c41f8   13 months ago   78MB
redis                           latest    590b81f2fea1   13 months ago   117MB
mysql                           latest    a82a8f162e18   13 months ago   586MB
bkarabacak/hello_world          latest    76331fac61d0   20 minutes ago  52.5MB  
hello_world                     latest    76331fac61d0   20 minutes ago  52.5MB
```

To run the container
```
docker run -d -p 8080:80 --name hello_world bkarabacak/hello_world:latest
```
- -d for detachment mode; container will be running in the background
- -p is to indicate internal and external ports, 8080 is for external , 80 is for internal port number
- 
You can see if the container is running 
```
docker ps 
```
Container will be listed with its informations
```
CONTAINER ID   IMAGE         COMMAND                  CREATED         STATUS         PORTS     NAMES  
836b6fac6a84   hello_world   "/docker-entrypoint.…"   2 seconds ago   Up 2 seconds   80/tcp    graci  
ous_herschel
```
To stop the container
```
docker stop CONTAINER_ID || docker stop CONTAINER_NAME
```
