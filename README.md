# CustomDashboarding_4_UCP
Example apps for SIMATIC Unified Comfort Panels, consisting of NodeRed, InfluxDB and Grafana.

### Prerequisites
- [x] You have installed both Docker and Docker Compose.
- [x] You have installed Industrial Edge App Publisher (IEAP), that can be [downloaded from SiePortal](https://support.industry.siemens.com/cs/pl/en/view/109778875) free of charge.
- [x] You have purchased the Edge for Unified Panels license.
- [x] Ypu are familiar with all necessary tools, including Docker (building images), Docker Compose (YAML file creation) and IEAP (generating APP file based on docker-compose.yaml).

### Helpful materials
- [Docker documentation](https://docs.docker.com/)
- [Docker Compose documentation](https://docs.docker.com/compose/)
- [Docker Hub - repository of ready-made Docker images](https://hub.docker.com/)
- [Node-Red documentation and tutorials](https://nodered.org/docs/)
- [InfluxDB documentation](https://www.influxdata.com/_resources/)
- [Grafana documentation](https://grafana.com/docs/grafana/latest/)
- [InfluxDB node for Node-Red](https://flows.nodered.org/node/node-red-contrib-influxdb)
- [How to configure InfluxDB (v2) connector in Grafana](https://docs.influxdata.com/influxdb/v2/tools/grafana/)

### Short steps:
1. Copy the repository to your local directory.
2. Go to the **NodeRed** catalog and build custom image using included **Dockerfile**. You can extend the file to install some extra nodes during image generation. They can also be installed later, as long as your UCP has Internet access.
3. Tag your NodeRed Docker image with:
```
nodered_ucp:latest
```
in order to use included docker-compose file (available in **NodeRed** catalog) without modifications. If you choose to use another tag, remember to adjust the line:
```
image: 'nodered_ucp:latest'
```
with your custom image name.
4. Pull another two images from Docker Hub in order to use them during Edge App deployment. Use commands:
```
docker image pull influxdb:2-alpine
docker image pull grafana/grafana:9.5.16
```
These images will be used for deploying InfluxDB and Grafana apps.
5. Use **Industrial Edge App Publisher** to create two separate app projects:
- First one costsits of one image. Name the app with the name of your choice (e.g. **NodeRed**) and use the NodeRed/docker-compose.yml file to build the app structure. Deploy the app.
- Second one consists of two images (it will be a multicontainer application) - InfluxDB for database and Grafana for dashboarding. Name he app with the name of your choice (e.g. **Data archive & visualization**) and use the InfluxDB_Grafana/docker-compose.yml file to build the ap structure. Deploy the app.
6. Import deployed apps to your UCP Edge Management and configure them based on their providers' tutorials.
7. Enjoy the Edge on your HMI panels!