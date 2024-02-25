# Dockerized-Zotero

This repository allows you to run the Zotero data server locally using docker containers, and easily build the Zotero client application. It is inspired by [ZotPrime](https://github.com/FiligranHQ/zotprime).

Before use, make sure you have Docker installed. For instructions on how to install Docker Desktop, see: [Install Docker Engine](https://docs.docker.com/engine/install).

## Zotero Server 

### Initial configuration 

1. Elasticsearch uses a _mmapfs_ directory by default to store its indices. The default operating system limits on mmap counts is likely to be too low, which may result in out of memory exceptions. On Linux, you can increase the limits by running the following command as root:

```bash
$ sudo sysctl -w vm.max_map_count=262144
```

To set this value permanently, update the _vm.max_map_count_ setting in _/etc/sysctl.conf_:

```bash
$ sudo echo "vm.max_map_count=262144" >> /etc/sysctl.conf
```

More info: [Elasticsearch Reference](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html#vm-max-map-count)


### Run Data Server

Download souce code and configure the server: 
```bash
$ sudo docker compose up -d
```

*Available endpoints*:

| Name          | URL                                           |
| ------------- | --------------------------------------------- |
| Zotero API    | http://localhost:8080                         |
| S3 Web UI     | http://localhost:8082                         |
| PHPMyAdmin    | http://localhost:8083                         |

*Default login/password*:

| Name          | Login                    | Password           |
| ------------- | ------------------------ | ------------------ |
| Zotero API    | admin                    | admin              |
| S3 Web UI     | zotero                   | zoterodocker       |
| PHPMyAdmin    | root                     | zotero             |


## Zotero Client 

### Build

Build Zotero Desktop App: 
```bash
$ sudo docker compose --profile build up [linux|windows]
```

The build will be placed in the _/client/zotero/app/staging_ folder in unpackaged form. The new files will be copied in this folder after finishing the compilation and closing zotero.

### First usage

*Run*:
```bash
$ ./staging/Zotero_VERSION/zotero(.exe)
```

*Connect with the default user and password*:

| Name          | Login                    | Password           |
| ------------- | ------------------------ | ------------------ |
| Zotero        | admin                    | admin              |

[comment]: ![Sync](./doc/sync.png)

