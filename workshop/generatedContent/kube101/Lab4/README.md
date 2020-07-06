# Lab 4: Use an ingress to expose the guestbook application

In this lab you'll deploy the same guestbook application we deployed in the previous labs, however, this time instead of accessing using a NodePort, you will access the application like a traditional web application by https and http URLs. As with lab 3, you will use resource files to speed the deployments along.

Before we work with the application we need to clone a github repo:

```shell
$ git clone https://github.com/IBMAppModernization/kube101.git
```

This repo contains the configuration files we'll use to deploy the pieces of the application.

Change directory by running the command `cd kube101/Lab4`. You will find all the
configurations files for this lab in that directory.

## 1. Set up the guestbook application

The guestbook application can use a redis database to persist guestbook entries, but this database is only discovered if the kubernetes service for it is active before you deploy the guestbook application. Begin by creating a deployment of redis and the service for redis, then create the guestbook application and the service for the guestbook app.

1. Create a redis deployment:

    ```console
    $ kubectl create -f redis-master-deployment.yaml
    ```

1. Check to see that redis server pod is running:

    ```console
    $ kubectl get pods -lapp=redis,role=master
    NAME                 READY     STATUS    RESTARTS   AGE
    redis-master-q9zg7   1/1       Running   0          2d
    ```

1. Create the service to access redis master:

    ```
    $ kubectl create -f redis-master-service.yaml
    ```

1. Create a guestbook deployment:

   ```console
   $ kubectl create -f guestbook-deployment.yaml
   deployment.apps/guestbook-v1 created
   ```

1. List the pod with label app=guestbook

   ```console 
   $ kubectl get pods -l app=guestbook
   ```

1. Finally, create the guestbook service using the same type of command
  we used when we created the Deployment:

   ```
   $ kubectl create -f guestbook-service.yaml
   ```

1. Test the service via the nodeport. Get the nodeport address and create the URL path, then paste that into a browser tab to verify the guestbook application is up and running.

    ```shell
    $ export NODEPORT=$(kubectl get svc guestbook -o=jsonpath='{.spec.ports[?(@.port==3000)].nodePort}')
    $ echo "http://$PROXYIP:$NODEPORT/"
    ```

## 2. Create a path-based ingress for the application

With the application up and running, the first ingress we will define will create a path below the proxy IP that will forward connections to the application. For the resource definition, the path which will be matched needs to be provided along with the backend service. Usually when using path-based application routing, it is important to add an annotation to rewrite the URL path before forwarding to the application.

Here is an example resource file for this type of ingress configuration:

````yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: guestbook-ingress-path
  annotations:
    ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /gb-user030
        backend:
          serviceName: guestbook
          servicePort: 3000
````

The path used will need to be parameterized for each user to avoid conflicts and overlaps. The example shows the path that would be used for user030. 

1. Parameterize your ingress file with your username:

    ```console
    $ sed -i"_x" "s/user###/$USERNAME/g" guestbook-ingress-path.yaml && rm guestbook-ingress-path.yaml_x
    ```

1. Create the ingress resource:

    ```console
    $ kubectl create -f guestbook-ingress-path.yaml
    ingress.extensions/guestbook-ingress-path created
    ```

1. Show the details of the created ingress:

    ```console
    $ kubectl describe ingress guestbook-ingress-path
    Name:             guestbook-ingress-path
    Namespace:        devnamespace030
    Address:          148.100.92.103
    Default backend:  default-http-backend:80 (<none>)
    Rules:
      Host  Path  Backends
      ----  ----  --------
      *
            /gb-user030   guestbook:3000 (<none>)
    Annotations:
      ingress.kubernetes.io/rewrite-target:  /
    Events:
      Type    Reason  Age   From                      Message
      ----    ------  ----  ----                      -------
      Normal  CREATE  45s   nginx-ingress-controller  Ingress devnamespace030/guestbook-ingress-path
      Normal  UPDATE  41s   nginx-ingress-controller  Ingress devnamespace030/guestbook-ingress-path
    ```

    Notice how this ingress resource is configured for any (*) host. One side effect of this is that if the default host has a TLS certificate configured, connections over https will be successfully accepted and then routed to the application. You will test this in the next step.

1. Connect to the application using the ingress controller, get the URL with the following command:

    ```echo https://$PROXYIP/gb-$USERNAME/```

    The guestbook application will be shown and any entries that you may have added before when accessing over the NodePort will be visible. You may leave the ingress defined at this time.

## 3. Create a host-based ingress for the application

Alternatively, you can also define an ingress for an application that exposes a specific virtual host name. In this case, there is usually a DNS CNAME configured that maps the desired virtual host name to the host name of the ingress node. For the sake of convenience, we will take advantage of the `xip.io` service which provides a DNS A record with the IP address for any name lookup of the form `foobar.my.ipv4.add.ress.xip.io`. For example the host `foobar.148.100.244.150.xip.io` will resolve to `148.100.244.150`.

Here is an example resource file for this type of ingress configuration:

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: guestbook-ingress-host
  labels:
    app: guestbook
spec:
  rules:
    - host: gb-user030.148.100.244.150.xip.io
      http:
        paths:
          - path: /
            backend:
              serviceName: guestbook
              servicePort: 3000
```

1. Parameterize the sample ingress file:

    ```console
    $ sed -i"_x" "s/user###/$USERNAME/g" guestbook-ingress-host.yaml && rm guestbook-ingress-host.yaml_x
    $ sed -i"_x" "s/PROXYIP/$PROXYIP/g" guestbook-ingress-host.yaml && rm guestbook-ingress-host.yaml_x
    ```

1. Create the ingress resource:

    ```console
    $ kubectl create -f guestbook-ingress-host.yaml
    ingress.extensions/guestbook-ingress-host created
    ```

1. Show the details of the created ingress:

    ```console
    $ kubectl describe ingress guestbook-ingress-host
    Name:             guestbook-ingress-host
    Namespace:        devnamespace030
    Address:          148.100.92.103
    Default backend:  default-http-backend:80 (<none>)
    Rules:
      Host                              Path  Backends
      ----                              ----  --------
      gb-user030.148.100.92.103.xip.io  
                                        /   guestbook:3000 (<none>)
    Annotations:
    Events:
      Type    Reason  Age        From                      Message
      ----    ------  ----       ----                      -------
      Normal  CREATE  6s         nginx-ingress-controller  Ingress devnamespace030/guestbook-ingress-host
      Normal  UPDATE  <invalid>  nginx-ingress-controller  Ingress devnamespace030/guestbook-ingress-host
    ```

    This time, there is a specific host target with a path of "/". Requests to other virtual host names will not be routed.

1. Connect to your guestbook application. Use the host value shown in the output from the `kubectl describe ingress guestbook-ingress-host` command. Should you use an http or https prefix? Experiment and see which on works. Why did one work and not the other? Is there a setup step that we did not perform for this scenario?

## Wrap up

Congratulations, you have successfully created ingress resources for a kubernetes application. In this lab we worked with features of the nginx service which is a very commonly used ingress controller. The nginx ingress controller is one of the internal ingress controllers in Kubernetes. However, there are many more [additional controllers](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/#additional-controllers) available for specific use cases.

That's the end of the lab. Now let's clean-up our environment:

```console
kubectl delete -f guestbook-deployment.yaml
kubectl delete -f guestbook-service.yaml
kubectl delete -f guestbook-ingress-host.yaml
kubectl delete -f guestbook-ingress-path.yaml
kubectl delete -f redis-master-service.yaml 
kubectl delete -f redis-master-deployment.yaml
```
