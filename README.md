# OpenShift Trojan Horse 🐴

## OpenShift Deployment

```powershell
(Get-Content rhel7.imagestream.yaml).Replace(
    "REPLACE_WITH_NAMESPACE", "your_namespace"
).Replace(
    "REPLACE_WITH_DOCKER_REPOSITORY", "your_docker_repository"
) |
oc apply -f -

(Get-Content rhel7-dropbear.imagestream.yaml).Replace(
    "REPLACE_WITH_NAMESPACE", "your_namespace"
) |
oc apply -f -

(Get-Content rhel7-dropbear.buildconfig.yaml).Replace(
    "REPLACE_WITH_NAMESPACE", "your_namespace"
).Replace(
    "REPLACE_WITH_HTTP_PROXY", "your_http_proxy"
).Replace(
    "REPLACE_WITH_HTTPS_PROXY", "your_https_proxy"
).Replace(
    "REPLACE_WITH_NO_PROXY", "your_no_proxy"
) |
oc apply -f -

(Get-Content trojan-horse.deploymentconfig.yaml).Replace(
    "REPLACE_WITH_NAMESPACE", "your_namespace"
) |
oc apply -f -

(Get-Content trojan-horse.service.yaml).Replace(
    "REPLACE_WITH_NAMESPACE", "your_namespace"
) |
oc apply -f -

(Get-Content trojan-horse.route.yaml).Replace(
    "REPLACE_WITH_NAMESPACE", "your_namespace"
).Replace(
    "REPLACE_WITH_TROJAN_HOSTNAME", "your_trojan_hostname"
) |
oc apply -f -
```

## `localhost` Port Forwarding

```powershell
oc port-forward REPLACE_WITH_POD_NAME 2222
plink -i user.ppk -P 2222 -R 0.0.0.0:8080:localhost:REPLACE_WITH_SERVICE_PORT -N user@localhost
```
