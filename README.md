# prom-grafana
Project to run prometheus and grafana locally

## Prerequisites
1. Install docker
2. Install docker-compose *linux only*  
    `sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`  
    If a different version is needed, substitute the 1.29.2 with desired version.
3. Set permission on docker-compose *linux only*
    `sudo chmod uao+x /usr/local/bin/docker-compose`
3. Get grafana docker image   
    `docker pull grafana/grafana`
4. Get prometheus docker image
    `docker pull prom/prometheus`

## Quick start

1. Run `CURRENT_ID="$(id -u):$(id -g)" docker-compose up`  
2. Navigate to http://localhost:9090 - prometheus
3. Navigate to http://localhost:3000 - grafana
4. Login to grafana using default username and password: admin/admin
5. Create a new dashboard and add a new panel
6. Select prometheus as data source
7. Enter the following query `rate(process_cpu_seconds_total[2m])` to see the rate of CPU use by the prometheus service over time.
Clean up containers `docker-compose rm`



## Configuring containers with compose.yaml
[Compose specification](https://github.com/compose-spec/compose-spec/blob/master/spec.md)


### grafana

https://grafana.com/docs/grafana/latest/administration/configuration/#configure-with-environment-variables
https://grafana.com/docs/grafana/latest/administration/configure-docker/

#### Data sources
The prometheus data source is defined in `provisioning/datasources/prometheus.yaml`.  If changes are needed for the prometheus data source, this yaml file should be updated.  

The `compose.yaml` file mounts the `provisioning` directory in this project to the [provisioning default path](https://grafana.com/docs/grafana/latest/administration/configure-docker/#default-paths) in the container.


#### Data storage

The `compose.yaml` file mounts the `data` directory in this project to the [data default path](https://grafana.com/docs/grafana/latest/administration/configure-docker/#default-paths) in the container.

### prometheus


