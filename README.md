# OpenShift ACME Controller Ansible Role

This Ansible role installs and configures the [OpenShift ACME controller](https://github.com/tnozicka/openshift-acme).

## Requirements

One of:

* OpenShift Container Platform 3.11 or later

## Role Variables

| Name                                   | Default value                     | Description                             |
|----------------------------------------|-----------------------------------|-----------------------------------------|
| appuio_openshift_acme_namespace        | `acme-controller`                 | Namespace to deploy the acme-controller |
| appuio_openshift_acme_endpoint         | `letsencrypt-staging`             | URL to ACME API endpoint                |
| appuio_openshift_acme_docker_image     | `quay.io/tnozicka/openshift-acme` | Docker Image to deploy                  |
| appuio_openshift_acme_docker_image_tag | `controller`                      | Tag of the Docker image to deploy       |
| appuio_openshift_acme_loglevel         | `4`                               | Loglevel (0-10)                         |
| appuio_openshift_acme_http_proxy       | `''`                              | HTTP and HTTPS proxy                    |
| appuio_openshift_acme_no_proxy         | `''`                              | List of domain elements or IP addresses |

## Dependencies

* [ansible-module-openshift](https://github.com/appuio/ansible-module-openshift)

## Example Usage

`meta/main.yml` of role using this role:

    dependencies:
    - src: git+https://github.com/appuio/ansible-role-openshift-acme
      version: v1.5.0

## Hints

### ACME Let's Encrypt URLs

The role supports aliases for URLs. These aliases make future URL changes
easier. The following aliases are included by default:

* `letsencrypt-staging`: https://acme-staging-v02.api.letsencrypt.org/directory
* `letsencrypt-production`: https://acme-v02.api.letsencrypt.org/directory

Either alias can be used instead of an actual URL in
`appuio_openshift_acme_endpoint`, i.e.:

```
appuio_openshift_acme_endpoint: letsencrypt-production
```

A URL may also be used directly, i.e.:

```
appuio_openshift_acme_endpoint: https://api.custom.example.com/
```

### OpenShift template

The OpenShift template under `files/acme-controller-template.yml` can also be used standalone.
Just invoke it with `oc process`. **Note**: You will need cluster-admin permissions to use
this template as it creates a `ClusterRole` object.

## License

Apache License Version 2.0

## Author Information

APPUiO Team <info@appuio.ch>
