# Kargo Demo for Flux

Two repos:

* [Flux Repo](https://github.com/christianh814/flux-kargo), which has all the installation components
* [This App repo](#kargo-demo-for-flux), which has all the application (GOBG) manifests for each env

# Insturcitons (High Level)

0. Create KIND Cluster

```shell
kind create cluster \
  --wait 120s \
  --config - <<EOF
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
name: kargo-quickstart
nodes:
- extraPortMappings:
  - containerPort: 31444 # Kargo dashboard
    hostPort: 31444
  - containerPort: 30081 # test application instance
    hostPort: 30081
  - containerPort: 30082 # UAT application instance
    hostPort: 30082
  - containerPort: 30083 # prod application instance
    hostPort: 30083
EOF
```

1. Bootstrap Flux

```shell
export GITHUB_TOKEN=$GH_TOKEN
flux bootstrap github --token-auth --owner christianh814 --personal --private --repository flux-kargo
```

2. Login to Kargo

First login to Kargo

```shell
kargo login --admin --insecure-skip-tls-verify https://localhost:31444
```

3. Create Secret: 

```shell
kargo create credentials \
--project=kargo-demo kargo-demo-repo \
--git --repo-url=https://github.com/christianh814/kargo-4-flux \
--username=christianh814 --password=${KARGO_GH_PAT}
```

4. Open UIs

* [Kargo UI](https://localhost:31444)
* [Test App](http://localhost:30081)
* [UAT App](http://localhost:30082)
* [Prod App](http://localhost:30083)

5. Make Change

Change the image

```shell
cd ./app/base
kustomize edit set image christianh814/gobg:green
cd -
```
