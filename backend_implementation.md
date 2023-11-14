# Backend implementation

Our backend and frontend will be using Docker and Docker compose for development and production environments.

### API Service
* Flask
* FlaskSQLAlchemy for ORM
* PostgreSQL

#### API Routes
**Users and Authentication**
 - POST /api/session/login - Logging into application
 - POST /api/session/logout - Logging out current application session

 
 - POST /api/users/ - Creating users.
 - PUT/PATCH /api/users/ - Modifying users.
 - POST /api/users/password-reset - Changing password for users

**Trips**
 -  POST /api/trips/ - Create new Trip
 -  PUT/PATCH /api/trips/ - Modifying Trips
 -  DELETE /api/trips/ - Deleting Trips
 -  POST /api/trips/generate - Generate an optimized trip

 

### OSRM / Optimizer Service
* Flask
* Optimizes the route after points are ran through OSRM
* Sends data back to the API service once finished
* MongoDB for storing previous points


### OSRM setup Dev
* First install ohio's map data `wget http://download.geofabrik.de/north-america/us/ohio-latest.osm.pbf`
* Pre process the data:
  * `docker run -t -v "${PWD}:/data" ghcr.io/project-osrm/osrm-backend osrm-extract -p /opt/car.lua /data/ohio-latest.osm.pbf || echo "osrm-extract failed"`
  * `docker run -t -v "${PWD}:/data" ghcr.io/project-osrm/osrm-backend osrm-partition /data/ohio-latest.osrm || echo "osrm-partition failed"`
  * `docker run -t -v "${PWD}:/data" ghcr.io/project-osrm/osrm-backend osrm-customize /data/ohio-latest.osrm || echo "osrm-customize failed"`
* Start the Server `docker run -t -i -p 5000:5000 -v "${PWD}:/data" ghcr.io/project-osrm/osrm-backend osrm-routed --algorithm mld /data/ohio-latest.osrm`
