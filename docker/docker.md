# Mounts/Volumes

Straight-forward folder mounting within docker

```
docker run --mount type=bind,source="/full/path/to/host/folder",target="/full/path/to/docker/folder" image_name
```

# Execute file within

```
docker run image_name sh /path/to/file.sh
```

# Docker ignore

`.dockerignore` works exactly like `.gitignore` in that it prevents builds from 
copying the files listed into the docker container

