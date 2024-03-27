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
- GET /api/ws - Websocket Upgrade endpoint (Handled by SocketIO)

### OSRM
* Standalone http server that generates the trip's correct order. Is requested to from the API service.
