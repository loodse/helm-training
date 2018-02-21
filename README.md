# Basic Helm Training

This training covers basic operations of Helm.

## Installing Tiller

In [Step 1](01-install-tiller/README.md) we learn how to install Tiller and bind him to a service account.

## Create your own Chart

In [Step 2](02-create-your-own-chart/README.md) we create our own first Chart based on a prepared K8s manifest.

## Install & upgrade your Chart

In [Step 3](03-install-your-own-chart/README.md) we are installing our Chart, afterwards upgrade it, do a rollback and then delete it.

## Additional commands

In [Step 4](04-additional-commands/README.md) are some additional & useful commands shown.

## Tipps & Tricks

### Tiller Namespace
During the tutorials I always use `--tiller-namespace`, you can instead set the environment variable `TILLER_NAMESPACE` to the correct value.
