docker-web-container
==================
## Reference
https://github.com/phusion/passenger-docker

## Usage

### Example

Build image
```shell
docker build -t <image name> .
```

Run container
```shell
docker run --name <container name> -p 10080:80 -p 10022:22 -d <image name>
```

