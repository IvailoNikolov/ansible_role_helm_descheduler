# ansible Role Helm Descheduler

[![Ansible Lint](https://github.com/Frantche/ansible_role_helm_descheduler/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/Frantche/ansible_role_helm_descheduler/actions/workflows/ansible-lint.yml)

## Description

Installs Descheduler helm chart on kubernetes cluster using helm

[Official documentation for Descheduler](https://github.com/kubernetes-sigs/descheduler)

## Roles variables

| Name                   | Description                                                                                                         | Value                              |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| helm_descheduler_name              | Release name to manage.                                                                                             | descheduler                      |
| helm_descheduler_chart_repo_url    | Chart repository URL where to locate the requested chart.                                                           | https://kubernetes-sigs.github.io/descheduler/ |
| helm_descheduler_chart_version     | Chart version to install. If this is not specified, the latest version is installed.                                | latest                            |
| helm_descheduler_chart_ref         | chart_reference on chart repository.                                                                                | descheduler                              |
| helm_descheduler_release_namespace | Kubernetes namespace where the chart should be installed.                                                           | descheduler                    |
| helm_descheduler_create_namespace  |                                                                                                                     | True                               |
| helm_descheduler_values            | Value to pass to chart.                                                                                             | {}                    |
| helm_descheduler_values_files      | Value files to pass to chart. Paths will be read from the target host’s filesystem, not the host running ansible.   | []                                 |
| helm_descheduler_wait              | When release_state is set to 'present' wait for minimal readiness if 'absent' wait for all ressources to be deleted | True                               |
| helm_descheduler_disable_hook      | Helm option to disable hook on install/upgrade/delete.                                                              | "no"                                |
| helm_descheduler_force             | Helm option to force reinstall, ignore on new install.                                                              | "no"                                |
| helm_descheduler_atomic            | If set, the installation process deletes the installation on failure.                                               | "no"                                |
| helm_descheduler_skip_crds         | Skip custom resource definitions when installing or upgrading.                                                      | "no"                                |
| helm_descheduler_update_repo_cache | Run helm repo update before the operation. Can be run as part of the package installation or as a separate step     | "no"                                |
| helm_descheduler_binary_path       | The path of a helm binary to use.                                                                                   | "/usr/local/bin"                   |
| helm_descheduler_context           | Helm option to specify which kubeconfig context to use.                                                             | default                            |
| helm_descheduler_kubeconfig        | Helm option to specify kubeconfig path to use.                                                                      | ~/.kube/config                     |
| helm_descheduler_validate_certs    | Whether or not to verify the API server’s SSL certificates.                                                         | "yes"                              |


## Requirements

create a file name "requirements.yml"
```yaml
---
collections:
    - name: kubernetes.core
      version: 2.3.2
    - name: git+https://github.com/IvailoNikolov/ansible_collection_helm_ingress.git master
roles:
  - name: frantchenco.ansible_role_helm_descheduler
    type: git
    src: https://github.com/IvailoNikolov/ansible_role_helm_descheduler.git
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
  - role: ivailo.ansible_role_helm_descheduler
```