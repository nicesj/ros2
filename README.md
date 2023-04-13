# ros2

ROS2

## Prepare the multi-target image build

```bash
 docker buildx create --name multi-builder --driver docker-container --bootstrap --use
```

## Build the ROS2 docker image

```bash
 docker buildx build -t registry.nicesj.com/ros2 --platform linux/amd64,linux/arm64 --push .
```

## Run the container

```bash
 docker run -it registry.nicesj.com/ros2:latest
```
