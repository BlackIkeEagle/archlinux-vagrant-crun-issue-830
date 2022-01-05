Steps to reproduce crun https://github.com/containers/crun/issues/830

```sh
vagrant up

vagrant ssh
[vagrant@archlinux ~]$ docker ps
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json": dial unix /var/run/docker.sock: connect: permission denied
[vagrant@archlinux ~]$ sudo -s
[root@archlinux vagrant]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@archlinux vagrant]# docker run --rm -it docker.io/library/alpine sh
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
59bf1c3509f3: Pull complete 
Digest: sha256:21a3deaa0d32a8057914f36584b5288d2e5ecc984380bc0118285c70fa8c9300
Status: Downloaded newer image for alpine:latest
docker: Error response from daemon: failed to create shim: OCI runtime create failed: sd-bus call: Invalid argument: unknown.
ERRO[0004] error waiting for container: context canceled
```

updated output with patch from https://github.com/containers/crun/pull/836

```sh
vagrant ssh
[vagrant@archlinux ~]$ sudo -s
[root@archlinux vagrant]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@archlinux vagrant]# docker run --rm -it docker.io/library/alpine sh
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
59bf1c3509f3: Pull complete
Digest: sha256:21a3deaa0d32a8057914f36584b5288d2e5ecc984380bc0118285c70fa8c9300
Status: Downloaded newer image for alpine:latest
docker: Error response from daemon: failed to create shim: OCI runtime create failed: unable to retrieve OCI runtime error (open /var/run/docker/containerd/daemon/io.containerd.runtime.v2.task/moby/3ff924a954975a6d0730f17e1d123faa5b78d69f1e0a744b149f9ce4e5e084eb/log.json: no such file or directory): fork/exec /usr/bin/crun: no such file or directory: <nil>: unknown.
ERRO[0004] error waiting for container: context canceled
```
