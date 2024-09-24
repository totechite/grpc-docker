# grpc-docker
gRPC builded docker images

**※If you need this solution, please manage the images yourself by forking the repository from this one.**

## Purpose
gRPC for PHP has a issue that building the module is pretty slow, and it hasn't solved. (ex. https://github.com/grpc/grpc/issues/34278)  
It affects 'Lead Time for Changes' of [four keys](https://www.atlassian.com/devops/frameworks/devops-metrics) on the products depend on gRPC.  

This images is the module completed has been builded.
By editting your Dockerfile as written below, it will be no wait for building.  

```Dockerfile
FROM php:8.3-fpm-bookworm

### Removal
# RUN pecl install grpc

### Get grpc.so without a wait time during building process.
COPY --from ghcr.io/totechite/grpc-docker:php-pecl-grpc1.66.0-bookworm /usr/local/lib/php/extensions/grpc.so /tmp/grpc.so
RUN mv /tmp/grpc.so $(php-config --extension-dir)/grpc.so
```


## Images

### Target Platforms

- linux/amd64
- linux/arm64


### Repository

- `ghcr.io/totechite/grpc-docker`

### Tags

#### PHP

- Tag Format
  - `<gRPC Version Prefix>-<libc Environment Suffix>`

| gRPC Version Prefixes | libc Environment Suffixes                |
| --------------------- | ---------------------------------------- |
| php-pecl-grpc1.66.0   | glibc2.31, bullseye, glibc2.36, bookworm |
| php-pecl-grpc1.65.5   | glibc2.31, bullseye, glibc2.36, bookworm |
| php-pecl-grpc1.64.1   | glibc2.31, bullseye, glibc2.36, bookworm |

- Example of full image name
  - `ghcr.io/totechite/grpc-docker:php-pecl-grpc1.66.0-glibc2.36`
  - `ghcr.io/totechite/grpc-docker:php-pecl-grpc1.66.0-bookworm`
