# Backend implementation
### OSRM setup Dev
* First install ohio's map data `wget http://download.geofabrik.de/north-america/us/ohio-latest.osm.pbf`
* Pre process the data:
  * `docker run -t -v "${PWD}:/data" ghcr.io/project-osrm/osrm-backend osrm-extract -p /opt/car.lua /data/ohio-latest.osm.pbf || echo "osrm-extract failed"`
  * `docker run -t -v "${PWD}:/data" ghcr.io/project-osrm/osrm-backend osrm-partition /data/ohio-latest.osrm || echo "osrm-partition failed"`
  * `docker run -t -v "${PWD}:/data" ghcr.io/project-osrm/osrm-backend osrm-customize /data/ohio-latest.osrm || echo "osrm-customize failed"`
* Start the Server `docker run -t -i -p 5000:5000 -v "${PWD}:/data" ghcr.io/project-osrm/osrm-backend osrm-routed --algorithm mld /data/ohio-latest.osrm`
