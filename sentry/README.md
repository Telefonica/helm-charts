Sentry Helm Chart
=================

What is Sentry? A platform to collect runtime errors in the deployed applications

Sentry runs on a shared cluster: internal-shared, currently hosted on Azure. Sentry is deployed using Terraform, as a Helm chart. It's designed to have multiple services:

* Sentry (Web + Worker + Cron)
* Snuba
* Symbolicator
* Kafka
* ClickHouse (with PVC): default Helm handling is that the PVC is reused, so you install/uninstall the chart without losing ClickHouse data.
* PostgreSQL (as a Service): current configuration uses Azure PostgreSQL, you just need to define the variables in values.yaml.

All variables in values.yaml are mandatory, all of them are fulfilled by Terraform when installing through Terraform, see [baikal-terraform](https://github.com/Telefonica/baikal-terraform).

If you want to do a manual deployment: edit values.yaml file, and install it:
```
helm install sentry ./sentry [--namespace sentry]
```
Then, remove it with:
```
helm uninstall sentry [--namespace sentry]
```