# helm-charts
Kubernetes applications

## How to add a new chart
```sh
$ helm package $YOUR_CHART_PATH/ # to build the tgz file
$ helm repo index . # create or update the index.yaml for repo
$ git add .
$ git commit -m 'Your commit message'
$ git push
```

## How to use this chart repo
```sh
$ helm repo add baikal 'https://telefonica.github.io/helm-charts/'
$ helm repo update
$ helm search <your-chart-name>
```
