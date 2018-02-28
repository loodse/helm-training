# Create your first Helm Chart

## Create your directory

`$ helm create NAME`

Helm helps you creating Helm charts, with the `create` command a directory
 will be created with some necessary files like the `Chart.yaml`, `values.yaml`, a `templates` directory, ...

In the following steps I assume, that you use `nginx` as Chart name

## Remove pre-created files

Helm will add a template for a deployment, ingress & service to the templates directory, let's remove them, we do not want to use them.

`$ rm nginx/templates/deployment.yaml nginx/templates/ingress.yaml nginx/templates/service.yaml`

## First steps

As a reference, there is a `nginx.yaml` in this directory, which contains a Deployment, Service, ConfigMap & a Secret Kubernetes Manifest, try to convert this to a Helm chart.

### Possible steps:

* create a file per Kubernetes entity
* use templating for often used identifiers & move them to the `values.yaml`
* move cross-referenced values like ports to the `values.yaml`
* the `b64enc` function could be useful for secrets
* use `helm template` to test your templates (maybe the first time after splitting up the manifest & before using any templating)

## Got lost?

If you got lost, have a look in `nginx-final`.

## Support

### Template

If you want to test your current chart, but don't want to install it you can use the template-function:

`$ helm template nginx/`

Outputs your rendered chart with the default `values.yaml`
If you're running Helm <= 2.7 you have to use the following command.

`$ helm install --debug --dry-run`

### Linting

Want to check if you're following the best practices, or if all your variables are set in the default `values.yaml`

`$ helm lint nginx/`
