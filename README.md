# kargo-simple-demo

2. Bootstrap Flux

```shell
export GITHUB_TOKEN=$GH_TOKEN
flux bootstrap github --token-auth --owner christianh814 --personal --private --repository kargo-4-flux
```

2. Create Kargo Project:

```shell
kargo create project kargo-demo
```

3. Create Secret: 

```shell
kargo create credentials \
--project=kargo-demo kargo-demo-repo \
--git --repo-url=https://github.com/christianh814/kargo-4-flux/ \
--username=christianh814 --password=${KARGO_GH_PAT}
```
