# Downloads and Installation

Reaper can be downloaded a number of ways.  DEB, RPM, and Docker images, and building from source are supported.

## Packages

Debian and RPM packages can be built from this project using Make, for example:

```bash
make deb
make rpm
```

## Docker


A [Docker](https://docs.docker.com/engine/installation/) build environment is
also provided to build the entire project and can be run by using
[Docker Compose](https://docs.docker.com/compose/install/):

```bash
docker-compose -f docker-build/docker-compose.yml build \
    && docker-compose -f docker-build/docker-compose.yml run build
```

The final packages will be located within:

```./packages/```


## Building from source

The easiest way to build is to use the following make command:

```bash
make package
```


To build Reaper without rebuilding the UI, run the following command : 

```mvn clean package```

To only regenerate the UI (requires npm and bower) : 

```mvn generate-sources -Pbuild-ui```

To rebuild both the UI and Reaper : 

```mvn clean package -Pbuild-ui```

To build the docker image :

```mvn clean package docker:build```

### Running Reaper

After modifying the `resource/cassandra-reaper.yaml` config file, Reaper can be started using the following command line :

```java -jar target/cassandra-reaper-X.X.X.jar server resource/cassandra-reaper.yaml```

Once started, the UI can be accessed through : http://127.0.0.1:8080/webui/

Reaper can also be accessed using the REST API exposed on port 8080, or using the command line tool `bin/spreaper`



## Install RPM or DEB package and run as a service

Install the RPM (Fedora based distros like RHEL or Centos) using : `sudo rpm -ivh reaper-*.*.*.x86_64.rpm`  
Install the DEB (Debian based distros like Ubuntu) using : `sudo dpkg -i reaper_*.*.*_amd64.deb`

The yaml file used by the service is located at `/etc/cassandra-reaper/cassandra-reaper.yaml` and alternate config templates can be found under `/etc/cassandra-reaper/configs`.
It is recommended to create a new file with your specific configuration and symlink it as `/etc/cassandra-reaper/cassandra-reaper.yaml` to avoid your configuration from being overwritten during upgrades.  
Adapt the config file to suit your setup and then run `sudo service cassandra-reaper start`.  
  
Log files can be found at `/var/log/cassandra-reaper.log` and `/var/log/cassandra-reaper.err`.  

Stop the service by running : `sudo service cassandra-reaper stop`  

