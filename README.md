## Kube-Warden

### Building from source

The default rule in the Makefile will build the binary and create a Docker image to run the application in. This can then be deployed to a running Kubernetes cluster.

For example, to build the container and start it, using your local kubectl config file:

```
$ make
env GOOS=linux go build -o bin/kube-warden
docker build .
Sending build context to Docker daemon 128.3 MB
Step 1/4 : FROM scratch
 --->
Step 2/4 : COPY bin/kube-warden .
 ---> afae5572b1d7
Removing intermediate container c5027eebb287
Step 3/4 : USER 65534:65534
 ---> Running in 678bbc54b4ab
 ---> 6c8ec9ad6ecd
Removing intermediate container 678bbc54b4ab
Step 4/4 : ENTRYPOINT /kube-warden
 ---> Running in caecd5b3fa55
 ---> 8bc45bf5cf2d
Removing intermediate container caecd5b3fa55
Successfully built 8bc45bf5cf2d

$ docker run -it -v $HOME/.kube/config:/.kube/config 8bc45bf5cf2d
Server is ready
```

If you just want the binary, run `make build`.
