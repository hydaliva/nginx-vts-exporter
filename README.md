#nginx-vts-exporter

Simple server that scrapes Nginx vts stats and exports them via HTTP for Prometheus consumption

#Dependency

* [nginx-module-vts](https://github.com/vozlt/nginx-module-vts)
* [Prometheus](https://prometheus.io/)
* [Golang](https://golang.org/)

#Download
Binary can be downloaded from `bin` directory.
Latest version v0.0.3

```
# SHA512 Sum
2004df2bd2a0dcca870bf259c6a2f49d58f2d759fa2a66d31f6a6d1876e08f774be122027eadbf5cb3b26042d998af6c1a5e3d80c41471a805415382e3f09f61  bin/nginx-vts-exporter
```

#Compile

```
$ ./build-binary.sh
```
This shell script above will build a temp Docker image with the binary and then
export the binary inside ./bin/ directory

#Run

```
$ nohup /bin/nginx-vts-exporter -nginx.scrape_uri=http://localhost/status/format/json
```

#Dockerized
To Dockerize this application yo need to pass two steps the build then the containerization.

## Environment variables
This image is configurable using different env variables

Variable name | Default     | Description
------------- | ----------- | --------------
NGINX_STATUS |  http://localhost/status/format/json | Nginx JSON format status page
METRICS_ENDPOINT | /metrics  | Metrics endpoint exportation URI
METRICS_ADDR | :9913 | Metrics exportation address:port
METRICS_NS | nginx | Prometheus metrics Namespaces


##Build
```
$ ./build-binary.sh
$ docker build -t vts-export .
```

##Run
```
docker run  -ti --rm --env NGIX_HOST="http://localhost/status/format/json" --env METRICS_NS="nginx_prod1" vts-export

```
