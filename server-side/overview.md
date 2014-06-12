# Server Side
## Overview

### Terms
Brief overview of terms we will use in the following documentation.

- **Headquarters**: A directory containing model files, model database, information on users. All information tying this server instance to you are contained in here.
- **Container**: A container is a virtual, isolated Linux os running on your server. For the use case of Yhat, we have containers that run one of two apps.
  - **Deployer**: You will only have one container running the deployer app. The deployer handles incoming requests to deploy a model, revert a model, and destroy a model. You can view more about the deployer on the [deployer page]().
  - **Predictor**: For each model you deploy, you will have a Predictor app running in a container for that model. The predictor is the REST API to your model, it handles HTTP requests as well as websockets. You can view more about the predictor on the [predictor page]().

- Packages Installed on Server & Use Case for them
  - nginx
    - How this connects to models and the admin app
  - git
    - About HQ
    - How this tracks versions and makes easy for moving to a new box
  - Node
  - Mongo
    - How users are stored on different enterprise types
  - sqlite3
    - Keeps tracks of model versions, etc
- Upstart Jobs
  - yhat (main job)
  - yhat_nginx
  - yhat_run_batch
  - yhat_reaper
  - Watchers
    - yhat_monitor_headquarters
    - yhat_monitor_orders
    - yhat_monitor_uploads
  - Individual Model Jobs
    - yhat_orders
    - yhat_deploy_order
  - Admin App Starters
    - yhat_dashboard
    - yhat_virtual_dashboard
- Yhat Go Server Client
  - Commands
    - each
    - command
    - here
- Container Apps
  - Deployer
    - handles deployments
    - reverting a model
    - deleting a model
  - Predictor
    - REST API to your model via websocket/HTTP protocol