# cis-girder-plugin
Adds API endpoints to Girder 2.3 for interacting with the Crops in Silico framework.

# Overview
This is a jumping-off point for creating a new server-side REST API plugin for Girder.

This plugin was developed using the Labs Workbench: https://www.workbench.nationaldataservice.org

# Usage
To use this plugin, simply load it into your Girder instance/image, login as an administratorm and navigate to the "Plugins" page

From here, you should see the new plugin listed and be offered an option to enable it.

If you do choose to enable it, you will be prompted to automatically restart/rebuild Girder.

## Without Docker
Simply clone this repo into your `/girder/plugins` directory - you may need to restart the server to see the new plugin.

## With Docker
This plugin will need to be copied into your Docker image for Girder.

Run the following command to produce a Docker image containing the plugin
```
docker build -t girder/girder:cis .
```

You can then run this image in place of your existing one to access the plugin.

# Development
1. Navigate and **Login** to the [Workbench](https://www.workbench.nationaldataservice.org)
2. Import the `girder23` application (seen below) into your Workbench **Catalog**
3. Add an instance of `girder23` and a Cloud9 Python IDE from the **Catalog**
4. On the **Dashboard**, edit your Cloud9 IDE's `Data` tab to mount `AppData/stackid-girder23` to `/workspace`
    * Make sure to substitute the stackid of your new `girder23` application
5. On the **Dashboard**, start up the Girder and Cloud9 IDE applications
6. Once Cloud9 is "Running" (e.g. turns green), click the link on the **Dashboard** to the IDE
6. Inside the IDE, use the terminal at the bottom to clone this repository into your Cloud9 `/workspace`

## The `girder23` Application
```
{
    "key": "girder23",
    "label": "Girder",
    "description": "Web-based data management platform.",
    "image": {
        "registry": "",
        "name": "girder/girder",
        "tags": [
            "2.3.0"
        ]
    },
    "display": "stack",
    "access": "external",
    "depends": [
        {
            "key": "mongo",
            "required": true
        }
    ],
    "args": [
        "-d",
        "mongodb://$(MONGO_PORT_27017_TCP_ADDR):$(MONGO_PORT_27017_TCP_PORT)/girder"
    ],
    "ports": [
        {
            "port": 8080,
            "protocol": "http",
            "contextPath": "/"
        }
    ],
    "repositories": [
        {
            "url": "https://github.com/girder/girder",
            "type": "git"
        }
    ],
    "readinessProbe": {
        "type": "",
        "path": "",
        "port": 0,
        "initialDelay": 0,
        "timeout": 0
    },
    "volumeMounts": [
        {
            "mountPath": "/girder/plugins/cis"
        }
    ],
    "resourceLimits": {
        "cpuMax": 500,
        "cpuDefault": 100,
        "memMax": 2000,
        "memDefault": 50
    },
    "tags": [
        "20",
        "2",
        "36"
    ],
    "info": "https://nationaldataservice.atlassian.net/wiki/display/NDSC/Girder",
    "authRequired": true
}
```
