# Install Tiller

## Prepare

To install Tiller in a seperated Namespace where he only can act, we have to do some preparations

### Create your namespace

```
$ TILLER_NAMESPACE=tiller-land
$ kubectl create namespace $TILLER_NAMESPACE
```

### Create a service account for the tiller

```
$ TILLER_SA=tiller-sa
$ kubectl create serviceaccount $TILLER_SA --namespace $TILLER_NAMESPACE
```

### Create a role for the tiller

Edit the `role.yaml` and set a name for the role (ROLENAME) and also replace NAMESPACE with the namespace, which should be used.

`$ kubectl create -f role.yaml`

#### GKE Rolebinding

If you tring that on GKE you will run in an error, before you have to grant your account cluster-admin rights.


Get your Account name.

```
$ gcloud info | grep Account

Account: [myname@example.org]
```

Afterwards create the clusterrole admin role binding.

```
$ kubectl create clusterrolebinding myname-cluster-admin-binding --clusterrole=cluster-admin --user=myname@example.org

Clusterrolebinding "myname-cluster-admin-binding" created
```

### Bind the role to the SA

Now you have to edit the `role-binding.yaml` and replace NAME, ROLENAME & NAMESPACE with the values from the previous steps and also give the binding a name (BINDINGNAME).

`$ kubectl create -f role-binding.yaml`

## Installing Helm

```
$ wget https://storage.googleapis.com/kubernetes-helm/helm-v2.12.3-linux-amd64.tar.gz
$ tar -zxvf helm-v2.12.3-linux-amd64.tar.gz
$ sudo mv linux-amd64/helm /usr/local/bin/helm
```

## Installing Tiller

### Installing Tiller with use of a ServiceAccount

After you prepare the serviceaccount, namespace, role & rolebinding, you can install tiller via the Helm CLI.

`$ helm init --service-account $TILLER_SA --tiller-namespace $TILLER_NAMESPACE`

### Test your tiller

Now your Tiller should work, let's install a NGinx to our namespace.

`$ helm install stable/phpbb --tiller-namespace $TILLER_NAMESPACE --namespace $TILLER_NAMESPACE`

This should work.

The `--tiller-namespace` is the namespace, where the tiller is running and `--namespace` where our application will be installed. In our example these have to be the same, because tiller is only allowed to act in his namespace.

### List your releases

`$ helm list --tiller-namespace $TILLER_NAMESPACE`

Will list your releases and the current versions.

### Delete your release

`$ helm delete --tiller-namespace $TILLER_NAMESPACE NAME-OF-THE-RELEASE`

After we tested tiller, let's delete our NGinx installation.
