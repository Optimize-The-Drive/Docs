# Optimize the Drive
###### Author: Nathan Dunn

### Overview
Users are able to create road trips by selecting locations on a map and/or searching for locations and having the application generate the best fit route. If users wish to save trips or make modifications to previous ones, they must sign up for account.

### Application Flow
* Users are greeted with a login screen. They can choose to sign up, login or continue without signing up.
* After signing up, logging in or continuing without signing up, the user lands on the main control page.
* In the main control page, the users are able to generate trips in the left control menu.
    * A description can be given for a trip.
    * The trip generation begins by asking users the start and endpoint of the trip.
    * They can pick and search intermediate locations for the trip on the map.
    * Once they are finished, they can click generate and the optimized trip is presented to them.
* If logged in, they can save these trips. Otherwise, they are prompted to sign up to enable this feature.
* If logged in, previous trips can be loaded and modified through the left control menu.
* Users can change their password or username.

# Dev Setup 

## Linting
### Front end

### Back end
* For back end linting we will force the use of `pylint`
* Follow this process:
  * Go to your vscode extentions and install `pylint` for your ide
  * Next change linting file to -> `ourlintingfile.txt`
  * Fix any changes the ide suggests and make sure to run pylint in the docker with:  
    `docker exec -it flask-api /bin/sh -c "pylint app.py"`
  
