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