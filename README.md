# OpenShift ACME Controller Ansible Role

This Ansible role installs and configures the [OpenShift ACME controller](https://github.com/tnozicka/openshift-acme).

## Requirements

One of:

* OpenShift Container Platform 3.5 or later
* OpenShift Origin 1.5 or later

## Role Variables

| Name             | Default value                   | Description                            |
|------------------|---------------------------------|----------------------------------------|
| namespace        | None (Required)                 | Namespace to deploy the acme-controler |
| acme_url         | Let's Encrypt Staging           | URL to ACME API endpoint               |
| docker_image     | docker.io/appuio/openshift-acme | Docker Image to deploy                 |
| docker_image_tag | latest                          | Tag of the Docker image to deploy      |

## Dependencies

* [ansible-module-openshift](https://github.com/appuio/ansible-module-openshift)

## Example Usage

`meta/main.yml` of role using this role:

    dependencies:
    - src: git+https://github.com/appuio/ansible-role-openshift-acme
      version: v1.0.0
        namespace: "acme-controller"

## Hints

### ACME Let's Encrypt URLs (`acme_url`)

* Staging: https://acme-staging.api.letsencrypt.org/directory
* Live: https://acme-v01.api.letsencrypt.org/directory

### Docker Image

There is a custom built docker image which is using the official golang image.
It's linked to the golang repository, so if there are updates, it will automatically
get rebuilt.

* Source: https://github.com/appuio/openshift-acme-docker
* Docker Hub: https://hub.docker.com/r/appuio/openshift-acme

### OpenShift template

The OpenShift template under `files/acme-controller-template.yml` can also be used standalone.
Just invoke it with `oc process`. **Note**: You will need cluster-admin permissions to use
this template as it creates a `ClusterRole` object.

## License

Apache License Version 2.0

## Author Information

APPUiO Team <info@appuio.ch>
