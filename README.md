# nested-helm-operator
An owncloud operator to demonstrate how to handle nested helm charts

## Creating a helm-based operator with dependencies

If your helm chart includes a dependencies.yaml/dependencies.lock file, the operator-sdk will pull the dependency when you create the project. That local copy will then be used by the operator. The structure looks like this:

    owncloud-operator
    ├── build
    │   └── Dockerfile
    ├── deploy
    │   ├── crds
    │   │   ├── cloud.owncloud.com_ownclouds_crd.yaml
    │   │   └── cloud.owncloud.com_v1alpha1_owncloud_cr.yaml
    │   ├── operator.yaml
    │   ├── role_binding.yaml
    │   ├── role.yaml
    │   └── service_account.yaml
    ├── helm-charts
    │   └── owncloud
    │       ├── Chart.lock
    │       ├── charts
    │       │   └── mariadb-5.11.3.tgz <===This is the pulled dependency
    │       ├── Chart.yaml
    │       ├── OWNERS
    │       ├── README.md
    │       ├── templates
    │       │   ├── deployment.yaml
    │       │   ├── externaldb-secrets.yaml
    │       │   ├── _helpers.tpl
    │       │   ├── ingress.yaml
    │       │   ├── NOTES.txt
    │       │   ├── owncloud-pvc.yaml
    │       │   ├── secrets.yaml
    │       │   └── svc.yaml
    │       └── values.yaml
    ├── licenses
    └── watches.yaml
    
In this example, we unzipped the folder to edit the parameters. We added a new value, nameOverride, to demonstrate the operator is using this local version of the helm chart.

    nameOverride: "example-nested-mariadb"
    
If you make changes, such as using a certified image instead, it will be in the newly-(re)built operator image. 

NOTE: Because the operator will only pull this local version, you'll need to update it manually and release an updated operator image if you want to use a newer version of your dependency.

