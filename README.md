# ansible Role Helm Cert Manager

[![Ansible Lint](https://github.com/Frantche/ansible_role_helm_cert_manager/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/Frantche/ansible_role_helm_cert_manager/actions/workflows/ansible-lint.yml)

## Description

Installs Cert-manager helm chart on kubernetes cluster using helm

## Roles variables

| Name                   | Description                                                                                                         | Value                              |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| helm_cert_manager_name              | Release name to manage.                                                                                             | cert_manager                      |
| helm_cert_manager_chart_repo_url    | Chart repository URL where to locate the requested chart.                                                           | https://charts.jetstack.io |
| helm_cert_manager_chart_version     | Chart version to install. If this is not specified, the latest version is installed.                                | latest                            |
| helm_cert_manager_chart_ref         | chart_reference on chart repository.                                                                                | ingress-cert_manager                              |
| helm_cert_manager_release_namespace | Kubernetes namespace where the chart should be installed.                                                           | ingress-cert_manager                     |
| helm_cert_manager_create_namespace  |                                                                                                                     | True                               |
| helm_cert_manager_values            | Value to pass to chart.                                                                                             | installCRDs: true                    |
| helm_cert_manager_values_files      | Value files to pass to chart. Paths will be read from the target host’s filesystem, not the host running ansible.   | []                                 |
| helm_cert_manager_wait              | When release_state is set to 'present' wait for minimal readiness if 'absent' wait for all ressources to be deleted | True                               |
| helm_cert_manager_disable_hook      | Helm option to disable hook on install/upgrade/delete.                                                              | no"                                |
| helm_cert_manager_force             | Helm option to force reinstall, ignore on new install.                                                              | no"                                |
| helm_cert_manager_atomic            | If set, the installation process deletes the installation on failure.                                               | no"                                |
| helm_cert_manager_skip_crds         | Skip custom resource definitions when installing or upgrading.                                                      | no"                                |
| helm_cert_manager_update_repo_cache | Run helm repo update before the operation. Can be run as part of the package installation or as a separate step     | no"                                |
| helm_cert_manager_binary_path       | The path of a helm binary to use.                                                                                   | "/usr/local/bin"                   |
| helm_cert_manager_context           | Helm option to specify which kubeconfig context to use.                                                             | default                            |
| helm_cert_manager_kubeconfig        | Helm option to specify kubeconfig path to use.                                                                      | ~/.kube/config                     |
| helm_cert_manager_validate_certs    | Whether or not to verify the API server’s SSL certificates.                                                         | "yes"                              |
| helm_cert_manager_install_prereq    | Check all pre requisites software are installed on the host who will perform command                                | True                               |
| acme_server_url    | Letsencrypt server url for http challenge                                | https://acme-staging-v02.api.letsencrypt.org/directory                               |
| acme_issue_email    | Email use with letsencrypt                               | john.d@google.com                               |

## Requirements

create a file name "requirements.yml"
```yaml
---
collections:
    - name: kubernetes.core
      version: 2.3.2
    - name: git+https://github.com/Frantche/ansible_collection_helm_wrapper.git,main
roles:
  - name: frantchenco.ansible_role_helm_cert_manager
    type: git
    src: https://github.com/Frantche/ansible_role_helm_cert_manager.git
    version: main
```

Install requirements with the Ansible Galaxy CLI:

```bash
ansible-galaxy install -r ./requirements.yml
```

## Playbook example


```yaml
---
- hosts: master[0]
  serial: 1
  roles:
  - role: frantchenco.ansible_role_helm_cert_manager
```