# Backend implementation

Our backend and frontend will be using Docker and Docker compose for development and production environments.

### API Service
* Flask
* FlaskSQLAlchemy for ORM
* PostgreSQL

#### API Routes
**Users and Authentication**
 - POST /api/auth/login - Logging into application
 - POST /api/auth/logout - Logging out current application session
 - POST /api/auth/refresh - Generates a new access token
 - POST /api/user/register - Creating user.
 - PATCH /api/user/me - Modifying yourself.
 - GET /api/user/me - Get own user.
 - POST /api/user/me/password-reset - Changing password
 - POST /api/user/me/verify - Verify user account
 - DELETE /api/user/me - Deleting accounts
 - GET /api/user/<id> - Get users. (TBD if we add ability for user visiblity / sharing)

**Trips**
 -  PUT/PATCH /api/trip/<id> - Modifying Trips
 -  DELETE /api/trip/<id> - Deleting Trips
 -  POST /api/trip/ - Generate an optimized trip
 -  GET /api/user/trip/(<id>) - GET trip(s) belonging to user.

**Websocket**
- GET /api/ws - Websocket Upgrade endpoint

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
