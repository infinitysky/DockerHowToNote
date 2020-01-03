# How to use the `startup service` in Docker?

Docker is a different "animal" than a virtual machine. Therefore anything that we experienced in a virtual machine will not 100% the same as the virtual machine. 
Please forget the "run level", it will not work in Docker.

## How to manage multiple services in a docker container?

Yes, we have an alternative way to manage it.
By using supervisor.

http://supervisord.org/

The `supervisor` is  ` A Process Control System`.

This python made tool will help us to handle the process/services.

### intall
by using apt CMD, we could install the supervisor in the docker container

```
apt-get install supervisor
```

### change supervisor configration

supervisor has config file, which is uder
`/etc/supervisor/conf.d/supervisord.conf`

If we want to add some service to let supervisor handling it, then we need to add config option inside the file.

for example
```

[supervisord]
nodaemon=true

[program:sshd]
command=/usr/sbin/sshd -D
autostart=true
startsecs=0

[program:mysqld]
command=/usr/bin/mysqld_safe
autorestart=true
startsecs=0

```

the format is :
```
[program:programName]
command= theServicesPath
autostart=true (if the services faill it will restart)
```

### usage
when we run the image to a container. we run the supervisor as the command inside the container.
```
sudo docker run -ti -p 80:80 -p 3306:3306 --restart=always --name server81  server01 /usr/bin/supervisord
```




