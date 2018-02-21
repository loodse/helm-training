# Install Tiller

## Prepare

To install Tiller in a seperated Namespace where he only can act, we have to do some preparations

### Create your namespace

`kubectl create namespace NAMESPACE`

Replace NAMESPACE with the name of the namespace you want to create 

### Create a service account for the tiller

`kubectl create serviceaccount NAME --namespace NAMESPACE`

Replace NAME with the name of the serviceaccount you want to create & NAMESPACE with the name of the namespace from the previously step.

### Create a role for the tiller

Edit the `role.yaml` and set a name for the role (ROLENAME) and also replace NAMESPACE with the namespace, which should be used.

`$ kubectl create -f role.yaml`

### Bind the role to the SA

Now you have to edit the `role-binding.yaml` and replace NAME, ROLENAME & NAMESPACE with the values from the previous steps and also give the binding a name (BINDINGNAME).

`$ kubectl create -f role-binding.yaml`

## Installing Tiller

### Installing Tiller with use of a ServiceAccount

After you prepare the serviceaccount, namespace, role & rolebinding, you can install tiller via the Helm CLI.

`$ helm init --service-account NAME --tiller-namespace NAMESPACE`

Replace `NAME` & `NAMESPACE` with the values from the previous steps.

### Test your tiller

Now your Tiller should work, let's install a NGinx to our namespace.

`$ helm install nginx --tiller-namespace NAMESPACE --namespace NAMESPACE`

This should work.

The `--tiller-namespace` is the namespace, where the tiller is running and `--namespace` where our application will be installed. In our example these have to be the same, because tiller is only allowed to act in his namespace.

### List your releases

`$ helm list --tiller-namespace NAMESPACE`

Will list your releases and the current versions.

### Delete your release

`$ helm delete --tiller-namespace NAMESPACE NAME-OF-THE-RELEASE`

After we tested tiller, let's delete our NGinx installation.
