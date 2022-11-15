# ansible Role Helm Wrapper

This Ansible Role aim to ease the use of helm chart with ansible by providing a fine wrapper around Helm installation and deletion from a kubernetes cluster.

The default value will install the Nginx helm chart from Bitnami with a replica set to two.

The ansible role is only compatible with kubernetes cluster configured via kubeconf file.

| Name                   | Description                                                                                                         | Value                              |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| helm_name              | Release name to manage.                                                                                             | nginx-bitnami                      |
| helm_chart_repo_url    | Chart repository URL where to locate the requested chart.                                                           | https://charts.bitnami.com/bitnami |
| helm_chart_version     | Chart version to install. If this is not specified, the latest version is installed.                                | 13.2.10                            |
| helm_chart_ref         | chart_reference on chart repository.                                                                                | nginx                              |
| helm_release_namespace | Kubernetes namespace where the chart should be installed.                                                           | nginx-bitnami                      |
| helm_create_namespace  |                                                                                                                     | True                               |
| helm_values            | Value to pass to chart.                                                                                             | replicaCount: 2                    |
| helm_values_files      | Value files to pass to chart. Paths will be read from the target host’s filesystem, not the host running ansible.   | []                                 |
| helm_wait              | When release_state is set to 'present' wait for minimal readiness if 'absent' wait for all ressources to be deleted | True                               |
| helm_disable_hook      | Helm option to disable hook on install/upgrade/delete.                                                              | no"                                |
| helm_force             | Helm option to force reinstall, ignore on new install.                                                              | no"                                |
| helm_atomic            | If set, the installation process deletes the installation on failure.                                               | no"                                |
| helm_skip_crds         | Skip custom resource definitions when installing or upgrading.                                                      | no"                                |
| helm_update_repo_cache | Run helm repo update before the operation. Can be run as part of the package installation or as a separate step     | no"                                |
| helm_binary_path       | The path of a helm binary to use.                                                                                   | "/usr/local/bin"                   |
| helm_context           | Helm option to specify which kubeconfig context to use.                                                             | default                            |
| helm_kubeconfig        | Helm option to specify kubeconfig path to use.                                                                      | ~/.kube/config                     |
| helm_validate_certs    | Whether or not to verify the API server’s SSL certificates.                                                         | "yes"                              |
| helm_install_prereq    | Check all pre requisites software are installed on the host who will perform command                                | True                               |


