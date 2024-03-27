# kargo-simple-demo

After installing **Kargo** and **Argo CD**

1. Create Kargo Project:

```shell
kargo create project kargo-demo
```

2. Create Secret: 

```shell
kargo create credentials \
--project=kargo-demo kargo-demo-repo \
--git --repo-url=https://github.com/christianh814/kargo-simple-demo/ \
--username=christianh814 --password=${KARGO_GH_PAT}
```

3. Deploy This Repo

```shell
kubectl apply -k  ./deploy/
```
