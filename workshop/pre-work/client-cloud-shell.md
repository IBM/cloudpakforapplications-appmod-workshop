# Pre-work

This section will guide you through the pre-requisites and setup of the environment used in this workshop labs. It is broken up into the following steps:

## Command Line Tools / Cloud Shell

Many of the labs will involve interacting with your cluster using command line tools. If you want to install the CLI tools directly on your machine follow the instructions on the `Access` page opened in the last section. If you do not have the command line tools installed on your machine, we recommend you use the [IBM Cloud Shell - https://shell.cloud.ibm.com/](https://shell.cloud.ibm.com/). The IBM Cloud Shell is preconfigured with the full IBM Cloud CLI and tons of plug-ins and tools that you can use to manage apps, resources, and infrastructure.

* From the [IBM Cloud Home Page](https://cloud.ibm.com), select the terminal icon in the upper right hand menu.

![Terminal Button](../.gitbook/generic/access-cloud-shell.png)

* It might take a few moments to create the instance and a new session which automatically logs you in through the IBM Cloud CLI.

![Cloud Shell](../.gitbook/images/grant-cluster/cloud-shell.png)

   > *Note: Ensure the cloud shell is using the same account where your cluster is provisioned. Check that the account name shown in the top right of the screen, next to `Current account` is the correct one.*

* Run the `ibmcloud ks clusters` command to view your cluster

   ```shell
   ibmcloud ks clusters
   ```

   > *Note: If no clusters are shown, make sure you are targeting the correct IBM account in the top right corner.*

* For convenience, export your cluster name as an environment variable.

   ```shell
   export CLUSTER_NAME=<your_cluster_name>
   ```

* We can now configure the `kubectl` cli available within the terminal for access to your cluster. If you stored your cluster name to an environment variable (ie. `$CLUSTER_NAME`), use that variable, otherwise copy and paste your cluster name from the previous commands output to the `$CLUSTER_NAME` portion below.

   ```shell
   ibmcloud ks cluster config --cluster $CLUSTER_NAME
   ```

* Verify access to the Kubernetes API by getting the namespaces.

   ```shell
   kubectl get namespace
   ```

* You should see output similar to the following, if so, then your're ready to continue.

```text
NAME              STATUS   AGE
default           Active   125m
ibm-cert-store    Active   121m
ibm-system        Active   124m
kube-node-lease   Active   125m
kube-public       Active   125m
kube-system       Active   125m
```

You should now be read to start with labs.

> Note: Every time you log in to the Cloud Shell (or your CLI tools), you must run the above commands to connect with the cluster in IBM Cloud.
