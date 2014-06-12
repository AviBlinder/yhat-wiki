# Server Side

## Packages

Along with our software, we install the following packages.

- [nginx](#nginx)
- [git](#git)
- [nodejs](#nodejs)
- [mongodb](#mongodb)
- [sqlite3](#sqlite3)

### nginx

Nginx is the webserver we use to route the incoming request. This handles requests for accessing the Dashboard, individual models, and the Deployer.
Each time a new model is deployed, it's route is passed to nginx so it can be routed accordingly. We go into more depth about that in the [Publish](#link to yhat go cli publish page) docs.

### git

Each Headquarters is a git repository. This can be pointing to a remote or local git repo. AWS AMI's are spun up and started pointing to a local git repository for the user's convienince.
Pointing the headquarters to a remote repository, makes it easier to easily spin up an exact same Yhat Server instance with the same models living on it.
Having the Headquarters as a git repo, makes it easy to track versions and revert models to previous versions.

### nodejs

The Dashboards are nodejs apps.

### mongodb

mongodb is used for the Yhat Cloud Users database. Because we run multiple instances of the Yhat Server to handle the amount of models Yhat Cloud manages, we needed a database we could access from all of them and easily interact with via the Admin Dashboard.

### sqlite3

sqlite3 is used to manage the Model database. It is great because it is a binary file saved in the Headquarters. This makes moving a Headquarters from one machine to another seamless.