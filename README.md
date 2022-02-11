# AMQ Broker / MQTT / Fuse

This has been tested on OpenShift 4.8, including Azure Red Hat OpenShift v4.8.

## Setup Broker

First, install the AMQ Broker operator.  You can do this through the OpenShift UI as an admin, or by executing the following command using the `oc` cli as a `cluster-admin`.

```
oc apply -k broker/operator
```

## Generate Certificates

For convenience, you can use the `cert.sh` script to generate certificates and add them to a `Secret`.  It assumes you are logged in ahead of time with the `oc` cli so that it can get the `apps` router url from your cluster.

From a Mac or Linux terminal, run:

```
./cert.sh mypassword
```

Where `mypassword` is any password you would like to use for the keystore.  This will use the Java keytool to generate a keystore and trustore, then encode them in a `secret` that will get added to the `/broker/instance` directory.  This secret is already added to the `.gitignore` file, so it will **not** be pushed to your git repo.

## Broker Instance

Once the operator is installed and you have generated your certificates/secret, you can create a Broker instance and the Topic.

```
oc apply -k broker/instance
```

## Setup OpenShift Pipelines

If you want to automate the build and deployment of the sample app, you can use OpenShift Pipelines.

First, install the OpenShift Pipelines operator.  You can do this through the OperatorHub catalog in the OpenShift Admin UI, or by running the following command as a `cluster-admin`.

```
oc apply -k pipelines/operator
```