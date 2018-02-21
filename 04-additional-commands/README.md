# Additional commands

## Helm Package

### Create a package

You can easily create a Helm package via the Helm CLI

`$ helm package NAME`

NAME is in this case the path to a Helm Chart, this chart has to be valid.

## Helm Repo 

### Add an repo

You can add additional repos to you Helm config

`$ helm repo add gitlab https://charts.gitlab.io`

### Update local repo cache

After you added a new repo, you should update your local repo cache

`$ helm repo update`

### Search the repos

Now you can easily search for Helm Package in the list of repos

`$ helm search gitlab`

### Create a Helm Repo index

You can generate a `index.yaml` for a Helm Repo via 

`$ helm repo index PATH`

Where the PATH should point to the location, where the packaged Helm Charts are.

`helm repo index` also provides a `--merge` & `--url` flag, to merge the new generated file with an existing `index.yaml` and to specify the full path of the packages.

## Dependencies

### Build dependcies

After you specified your dependcies in your `requirements.yaml`, you can run 

`$ helm dependency build`

which will build you Helm Chart and pin the versions of your dependcies in the `requirements.lock`

### Update dependcies

To update you depencies, run 

`$ helm dependency update`

## Install a Chart

### Upgrade --install

If you want to integrate Helm in a pipeline and you are not sure, if Release is already installed, I recommend a 

`$ helm upgrage --install`

which will either upgrade or install a Release.
