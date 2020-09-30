# Helm Configuration

For the Helm labs of this workshop we will be using Helm Version 3. If you are running the labs using the IBM Cloud Shell, we need to complete a couple of setup steps before we proceed. This section is broken up into the following steps:

1. [Access the Cloud Shell](#1-access-the-cloud-shell)
1. [Install Helm Version 3](#2-install-helm-version-3)
1. [Configure Kubectl](#3-configure-kubectl)

## 1. Access the Cloud Shell

If you do not already have it open from the workshop setup section, go ahead and open the Cloud shell.

1. From the [IBM Cloud Home Page](https://cloud.ibm.com), select the terminal icon in the upper lefthand menu.

![Terminal Button](../.gitbook/generic/access-cloud-shell.png)

> *Note: Ensure the cloud shell is using the same account where your cluster is provisioned. Ensure that the account name shown in the top right of the screen, next to `Current account` is the correct one.*

## 2. Install Operator SDK

The Cloud Shell comes with several tools/libraries. For the lab, we will use the `operator-sdk` cli, which depends on `Go` to be installed. To check if both tools are installed in your shell, runn the following commands.

```shell
go version
```

```shell
operator-sdk version
```

If you see a `command not found` error, you will need to install both. For detailed installation instructions go [here](https://sdk.operatorframework.io/docs/install-operator-sdk/).

The version of the operator SDK used in the lab is 0.18.2. If the version shown from the above command is not 0.18.2, we need to install it.

```shell
curl -LO https://github.com/operator-framework/operator-sdk/releases/download/v0.18.2/operator-sdk-v0.18.2-x86_64-linux-gnu
```

```shell
chmod +x operator-sdk-v0.18.2-x86_64-linux-gnu
```

```shell
mkdir $HOME/operatorsdk0182
```

```shell
cp operator-sdk-v0.18.2-x86_64-linux-gnu $HOME/operatorsdk0182/operator-sdk
```

```shell
rm operator-sdk-v0.18.2-x86_64-linux-gnu
```

```sh
echo 'export PATH=$HOME/operatorsdk0182:$PATH' > .bash_profile
```

```sh
source .bash_profile
```

Check again,
```shell
operator-sdk version
```

## 3. Configure Kubectl

If you have not setup your kubectl to access your cluster, you can do so in the Cloud Shell.

1. Run the `ibmcloud ks clusters` command to verify the terminal and setup for access to the cluster

   ```shell
   ibmcloud ks clusters
   ```

1. Configure the `kubectl` cli available within the terminal for access to your cluster. If you previously stored your cluster name to an environment variable, use that (ie. `$CLUSTER_NAME`), otherwise copy and paste your cluster name from the previous commands output to the `$CLUSTER_NAME` portion below.

   ```shell
   ibmcloud ks cluster config --cluster $CLUSTER_NAME
   ```

1. Verify access to the Kubernetes API by getting the namespaces.

   ```shell
   kubectl get namespace
   ```

1. You should see output similar to the following, if so, then your're ready to continue.

```text
NAME              STATUS   AGE
default           Active   125m
ibm-cert-store    Active   121m
ibm-system        Active   124m
kube-node-lease   Active   125m
kube-public       Active   125m
kube-system       Active   125m
```
