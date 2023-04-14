# ros2

ROS2

## Prepare the multi-target image build

```bash
$ docker buildx create --name multi-builder --driver docker-container --bootstrap --use
```

## Build the ROS2 docker image

```bash
$ docker buildx build -t registry.nicesj.com/ros2 --platform linux/amd64,linux/arm64 --push .
```

## Run the container

You may be need to add the following environment values for GUI tools of ROS2

 * QT\_QPA_PLATFORM
   - wayland

 * XDG\_RUNTIME\_DIR
   - "/tmp"

 * WAYLAND\_DISPLAY
   - ${WAYLAND\_DISPLAY}

Also, you may need to do volume-mount for the wayland socket file

 * Mount the "${XDG\_RUNTIME\_DIR}/${WAYLAND\_DISPLAY}" on "/tmp/${WAYLAND\_DISPLAY}" in the container
   - Note that the "/tmp" directory were used to set the XDG\_RUNTIME\_DIR environment variable

```bash
$ docker run -e QT_QPA_PLATFORM=wayland  -e XDG_RUNTIME_DIR=/tmp -e WAYLAND_DISPLAY=$WAYLAND_DISPLAY -v $XDG_RUNTIME_DIR/$WAYLAND_DISPLAY:/tmp/$WAYLAND_DISPLAY -it registry.nicesj.com/ros2:latest
```
