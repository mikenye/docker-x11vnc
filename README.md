# THIS IMAGE IS DEPRECATED! #

Please use the significantly better jlesage/baseimage-gui image instead. Thanks.

--------------------

# docker-x11vnc
Docker container for X window client, accessed via VNC. Supports multiple resolutions and on-the-fly resolution changes.

# Launching the container
```
docker run \
-d \
--restart=always \
--name xserver \
-p 6000:6000/tcp \
-p 5900:5900/tcp \
-e TZ="Australia/Perth" \
-h xserver \
x11vnc
```

# Set VNC Password
```
docker exec -it xserver x11vnc --storepasswd
```

# Add resolutions
```
docker exec -it xserver addresolution 1280x778 1280 778
```
Once resolutions are added, right-click the background of the X session, choose "Screen Layout Editor". Go to "Outputs" > "screen" > "Resolution" and select your resolution.

# Run applications and display in this container
Set your $DISPLAY variable to be your docker host's IP address ie: <IP>:0.0.
For example:
```
DISPLAY=192.168.9.22:0.0
```
  
Example: Running the official Handbrake container, and display on this X server:
```
docker run -d --name handbrake -h handbrake -e DISPLAY=$DISPLAY handbrake:nightly
```
