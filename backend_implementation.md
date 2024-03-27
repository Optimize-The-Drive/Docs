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

*NOTE: the reason I use /user/me notation in the url is to safeguard user specific information. I can verify a request belonging to a user using the JWT identity and don't need to write a middleware to check if a user has access to a specific user resource.*

**Trips**
 -  PUT/PATCH /api/trip/<id> - Modifying Trips
 -  DELETE /api/trip/<id> - Deleting Trips
 -  GET /api/trip/ - Get all trips. (Will be filtered based on the resources a user has access to) 
 -  POST /api/trip/ - Generate an a trip with no points

**Websocket**
- GET /api/ws - Websocket Upgrade endpoint (Handled by SocketIO)
- events:
   * generate_points (client side emit)
   * generate_points_res (server side emit)

### OSRM
* Standalone http server that generates the trip's correct order. Is requested to from the API service.
