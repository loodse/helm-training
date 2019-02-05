# Install your own Chart

After we learned how to install the Tiller which is using a ServiceAccount and get in touch with Chart templates, let's install our nginx Chart.

## Install ngix

First let's install the nginx Chart with an own defined name.

`$ helm install --tiller-namespace $TILLER_NAMESPACE --namespace $TILLER_NAMESPACE --name $NAME nginx/`

Hint: we want to set the namespace during the installation & don't want to hardcode them in the templates.

## Upgrade an installation

With Helm we also can upgrade deployments.

`$ helm upgrade --tiller-namespace $TILLER_NAMESPACE --namespace $TILLER_NAMESPACE $NAME nginx -f upgrade.yaml`

I prepared an other files with values, called `upgrade.yaml` this will override the defaults value & and upgrade our release.

## List a releases

Now you should see that your release jumped to the next revision

`$ helm ls --tiller-namespace $TILLER_NAMESPACE`

## Rollback a release

If you want to rollback a release, Helm will also handle all steps for you, just execute

`$ helm rollback --tiller-namespace $TILLER_NAMESPACE $NAME $REVISION`

Where NAME is the name of the release you set and REVISION the number of the revision you want to rollback.

## Delete a release

Helm lets you also delete a release

`$ helm delete --tiller-namespace $TILLER_NAMESPACE $NAME`

