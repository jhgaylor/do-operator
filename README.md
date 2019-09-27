A Kubernetes [operator](https://github.com/operator-framework/operator-sdk) for provisioning and managing DO database instances.

[![CircleCI](https://circleci.com/gh/digitalocean/do-operator.svg?style=svg)](https://circleci.com/gh/digitalocean/do-operator)

## Usage

First create a `Secret` containing your DigitalOcean API token:
```sh
kubectl create secret generic do-operator --from-literal="DIGITALOCEAN_ACCESS_TOKEN=${DIGITALOCEAN_ACCESS_TOKEN}"
```

Install the latest release into your cluster with:
```
kubectl apply -f https://raw.githubusercontent.com/digitalocean/do-operator/master/releases/v0.0.2/manifest.yaml
```

Create a `Database` object:
```yaml
apiVersion: doop.do.co/v1alpha1
kind: Database
metadata:
  name: example
spec:
  name: example
  engine: redis
  version: "5"
  size: db-s-2vcpu-4gb
  region: sfo2
  num_nodes: 2
  tags:
  - test
  - doop
```

Check the status:
```sh
kubectl describe database example
```

A couple secrets will be created for each `Database` instance; `example-connection` and `example-private-connection`.
