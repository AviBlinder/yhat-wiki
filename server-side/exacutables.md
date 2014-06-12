## Scripts

- [`yhat-config-storage`](#yhat-config-storage)
- [`yhat-memory-usage`](#yhat-memory-usage)
- [`yhat-server-status`](#yhat-server-status)
- [`yhat-upgrade`](#yhat-upgrade)
- [`yhat-watch`](#yhat-watch)

#### `yhat-config-storage`
Configure a local Headquarters. This is only necessary for using a local repo. If remote, then you'll need to add the required SSH KEY via [`yhat add-private-key`](#add-private-key) and use [`yhat headquarters`](#headquarters).

#### `yhat-memory-usage`
Returns the memory usage for all running containers.

#### `yhat-server-status`
Compares the number of `deploy_orders` jobs that are processing and the number of running docker containers to see if all orders are up. Also checks the status, be it online, failed, or building, for each model.

#### `yhat-upgrade`
Upgrades your entire Yhat server. You should first run `yhat stop` and make sure everything has stopped running before upgrading.

#### `yhat-watch`
Monitors the status of all running containers.


## Yhat Server Client

This is a command line tool for performing various functions. It is written in go. The commands available are listed below. I grouped them according to the purpose they serve.

- [`help`](#help)

##### [Basic](#basic)
- [`start`](#start)
- [`stop`](#stop)
- [`restart`](#restart)
- [`status`](#status)
- [`update`](#update)
- [`upgrade-interface`](#upgrade-interface)
- [`build-yhat-base`](#build-yhat-base)

##### [Setup](#setup)
- [`register`](#register)
- [`add-private-key`](#add-private-key)
- [`headquarters`](#headquarters)
- [`config-ec2`](#config-ec2)
- [`set-container-dns`](#set-container-dns)

##### [Users](#users)
- [`add-user`](#add-user)
- [`find-user`](#find-user)
- [`change-user-apikey`](#change-user-apikey)
- [`change-user-password`](#change-user-password)

##### [Model Deployment](#model-deployment)
- [`deploy`](#deploy)
- [`containerize`](#containerize)
- [`publish`](#publish)
- [`is-app-up`](#is-app-up)
- [`unpublish`](#unpublish)
- [`destroy`](#destroy)
- [`large-model-deploy`](#large-model-deploy)

#### `help`
If ever in need you can run `yhat help` or `yhat <command> --help` to view the usage on a command.

### Basic
These commands control starting, stopping, and updating the Dashboards, Deployer, & Predictor apps.

If you are looking to upgrade all of Yhat on your server please see the [yhat-upgrade](#yhat-upgrade). This is because the command line cannot update itself, the binary file, while it is running ;).


#### `start`
Starts the `yhat` upstart job which starts all of Yhat.

#### `stop`
Stops the `yhat` upstart job, which triggers the stopping of all other Yhat services.

#### `restart`
Restarts the `yhat` upstart job, which triggers a restart of all other Yhat services.

#### `status`
Returns a status of all Yhat services. Includes information on if the status is running or stopped.

#### `update`
Updates the deployer & predictor applications to the latest versions.

#### `upgrade-interface`
Upgrades Yhat Dashboards to the latest versions.

#### `build-yhat-base`
Rebuilds the yhat/base container image which is used as the base for the Deployer & Predictor containers.

### Setup

#### `register`
Registers a product key to a specific organization which activates the Yhat server.

#### `add-private-key`
Adds your private key to the server so Yhat can pull/push your Headquarters git repo to a private git repo.

#### `headquarters`
Specifies the Headquarters git url which can be a private, remote repo if you added the private key via `add-private-key`.

#### `config-ec2`
Checks if the server is an Amazon EC2 instance. If so, it grabs the product key and Headquarters from the server's user-data.

#### `set-container-dns`
Sets the dns for all containers, this can be an internal DNS if hosted behind a firewall.

### Users

#### `add-user`
Adds a user to the Yhat server.

#### `find-user`
Queries for a user based off their username

#### `change-user-apikey`
Generate a new apikey for user

#### `change-user-password`
Change a user password

### Model Deployment

#### `deploy`
Deploys a container.

1) Loads the Deployer or Predictor app depending on the orders.
2) Builds the Deployer or Predictor app container image if it has not done so already.
3) Runs a container with the previous image and the specific model information.
4) Publishes the container route to nginx.
5) Checks if the container is up and stable.

#### `containerize`
Creates a docker container for a given git repo/app. This is step 2, & 3 of `deploy`.

#### `publish`
Publishes a container's route to nginx. This is step 4 of `deploy`.

#### `is-app-up`
Checks if a container is up and stable. This is step 5 of `deploy`.

#### `unpublish`
Removes an nginx route for a container.

#### `destroy`
Stops a container.

#### `large-model-deploy`
Prepares large model files for deployment.
