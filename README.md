redis-desktop-manager-docker
============================

Install Docker
--------------
https://docs.docker.com/install/linux/docker-ce/centos/
https://docs.docker.com/install/linux/docker-ce/ubuntu/
etc...


Pulling RDM image
--------------
```
sudo su

docker pull benoitg/redis-desktop-manager
xhost +
docker run -it --rm \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    -v $HOME/.rdm:/root/.rdm \
    -e DISPLAY=$DISPLAY \
    --device /dev/dri \
    -e SSH_AUTH_SOCK \
    -v $SSH_AUTH_SOCK:$SSH_AUTH_SOCK \
    --name redis-desktop-manager \
    benoitg/redis-desktop-manager

# Run
docker start rdm
```

Optional: Adding RDM icon  to applications menu
-------------------------------------------------
```
wget https://redislabs.com/wp-content/themes/redislabs/assets/images/redis-logo-stack.png -O /usr/share/icons/redis-logo-stack.png
echo "[Desktop Entry]
Version=1.0
Name=Redis Desktop Manager
Exec=gksudo -k -u root docker start rdm
Type=Application
Icon=/usr/share/icons/redis-logo-stack.png
StartupNotify=true" > /usr/share/applications/rdm.desktop

```

