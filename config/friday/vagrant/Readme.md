## jenkins requirements ##

nexus plugin , blue ocean , pipeline utilites steps , ansible
nexus credentials
mvn home tool
parametrize pipeline job


## nexus requirements ##

add security realm `docker token bearer`
create hosted repo called `docker`


## tds docker daemon config ##

```bash {
  "insecure-registries": [
    "172.16.11.100:8083"
],
  "disable-legacy-registry":true,
  "hosts": ["tcp://0.0.0.0:2375", "unix:///var/run/docker.sock"],
  "metrics-addr" : "0.0.0.0:9323",
  "experimental" : true
}
```

## jnx docker daemon config ##
```sh {
  "insecure-registries": [
   "localhost:8082",
   "localhost:8083",
   "localhost:8084"

 ],
 "disable-legacy-registry":true
}
````

## jnx/tds allow docker jenkins/vagrant users ##

```sh  
sudo groupadd docker
sudo usermod -a -G docker jenkins
sudo usermod -a -G docker vagrant
```
reboot the server using init 6 or logout from machine
