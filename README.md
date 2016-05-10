Quobyte volume plug-in for Docker
=================================

Setup:
* create a user in Quobyte for the plug-in:
```
 qmgmt -u <api-url> user config add docker <email>
```

* set mandatory configuration in environment
```
export QUOBYTE_API_USER=docker
export QUOBYTE_API_PASSWORD=...
export QUOBYTE_API_URL=http://<host>:7860/
# host[:port][,host:port] or SRV record name
export QUOBYTE_REGISTRY=quobyte.corp
```

* Start the plug-in as root (with above environment)
``` 
quobyte-docker-volume.py 
```

Examples:

```
# docker volume create --driver quobyte --name <volumename> --opt volume_config=MyConfig
# docker volume create --driver quobyte --name <volumename>
# docker volume rm <volumename>
# docker run --volume-driver=quobyte -v <quobyte volumename>:path
```

* Install systemd files
Set the variables in systemd/docker-quobyte.env.sample

```
cp systemd/docker-quobyte.env.sample /etc/quobyte/docker-quobyte.env
cp quobyte-docker-volume.py /usr/libexec/docker/
cp systemd/* /lib/systemd/system

systemctl enable docker-quobyte-plugin
systemctl status docker-quobyte-plugin
```
