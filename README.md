# AMQ Broker / MQTT / Fuse

This has been tested on OpenShift 4.8, including Azure Red Hat OpenShift v4.8.

## Setup Broker

First, install the AMQ Broker operator.  You can do this through the OpenShift UI as an admin, or by executing the following command using the `oc` cli as a `cluster-admin`.

```
oc apply -k broker/operator
```

Once the operator is installed, you can create a Broker instance and the Topic.

```
oc apply -k broker/instance
```

## Setup OpenShift Pipelines

If you want to automate the build and deployment of the sample app, you can use OpenShift Pipelines.

First, install the OpenShift Pipelines operator.  You can do this through the OperatorHub catalog in the OpenShift Admin UI, or by running the following command as a `cluster-admin`.

```
oc apply -k pipelines/operator
```