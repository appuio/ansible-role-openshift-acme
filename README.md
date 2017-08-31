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
| acme_url         | Let's Encrypt Staging           |                                        |
| docker_image     | docker.io/appuio/openshift-acme |                                        |
| docker_image_tag | latest                          |                                        |

## Dependencies

* [ansible-module-openshift](https://github.com/appuio/ansible-module-openshift)

## Example Usage

`meta/main.yml` of role using this role:

    dependencies:
    - src: git+https://github.com/appuio/ansible-role-openshift-acme
      version: v1.0.0
        namespace: "acme-controller"

## License

Apache License Version 2.0

## Author Information

APPUiO Team <info@appuio.ch>
