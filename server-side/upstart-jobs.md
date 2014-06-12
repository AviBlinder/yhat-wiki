# Server Side

## Upstart Jobs

Upstart is an event-based replacement for the /sbin/init daemon which handles starting of tasks and services during boot, stopping them during shutdown and supervising them while the system is running.

We have several so I grouped them into categories.


- [`yhat`](#yhat)
- [`yhat_nginx`](#yhat_nginx)
- [`yhat_reaper`](#yhat_reaper)

- ##### [Watchers](#watchers)
    - [`yhat_monitor_headquarters`](#yhat_monitor_headquarters)
    - [`yhat_monitor_orders`](#yhat_monitor_orders)
    - [`yhat_monitor_uploads`](#yhat_monitor_uploads)

- ##### [Individual Jobs](#individual-jobs)
    - [`yhat_orders`](#yhat_orders)
    - [`yhat_deploy_order`](#yhat_deploy_order)
    - [`yhat_run_batch`](#yhat_run_batch)


- ##### [Dashboards](#dashboards)
    - [`yhat_dashboard`](#yhat_dashboard)
    - [`yhat_virtual_dashboard`](#yhat_virtual_dashboard)


#### `yhat`

This is the main loop. It starts on boot. It fires every 5 seconds (this 5 second pulse will heretoforth be referred to as `yhat_pulse`) and triggers the [`Watchers`](#watchers).

#### `yhat_nginx`

This is nginx web server. It is started on `yhat` start.

#### `yhat_reaper`

This is a cleaner-upper. It runs via a cronjob every ten minutes. It removes containers of models that have been deleted.

### Watchers

The "Watchers" are jobs that are triggered on `yhat_pulse`.

#### `yhat_monitor_headquarters`
This compares the centralized Headquarters git repo to the local repo. If a change is detected it pushes/pulls the changes to the local repo.

#### `yhat_monitor_orders`
Each Headquarters has a directory structure like the following:

```tex
.
├── uploads/
├── deployer
│   └── orders
├── username2
│   └── models
│       ├── HelloPython
│       │   ├── bundle.json
│       │   └── orders
│       └── HelloWorld
│           ├── bundle.json
│           └── orders
├── username1
│   └── models
│       ├── HelloR
│       │   ├── bundle.json
│       │   └── orders
└── yhat.db
```

This looks at each "orders" file in the Headquarters that are generated for each model. When a new one is found it triggers `yhat_orders` for that model.

#### `yhat_monitor_uploads`
This handles any models that contain objects that are too large to be uploaded via basic HTTP. This job watches the uploads directory in the Headquarters for .yhat files. If it finds one, it deploys the model. For more on the deployment process see [large model deploy](#link to yhat cli large model deploy function).

### Individual Jobs

#### `yhat_orders`
This reads a new orders file and clones the directory pertaining to that model locally. Once it has everything in place, it triggers `yhat_deploy_order`.

#### `yhat_deploy_order`
This deploys a model with the Yhat Server Client command [deploy](#link to deploy function).

#### `yhat_run_batch`
This handles running an entire CSV file through a model. It does this by chunking the file into parts and running each part through the model.

### Dashboards
Both dashboards are started on `yhat` start.

#### `yhat_dashboard`
This starts the Admin Dashboard node app.

#### `yhat_virtual_dashboard`
This starts the Setup Dashboard node app.