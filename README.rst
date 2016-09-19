OpenStack-Ansible Prometheus Server
###################################

Ansible role that installs and configures Prometheus Monitoring Server. Prometheus
is installed onto a host that is part of the prometheus-infra_hosts group and
listens on port 9090 by default.

Required Variables
==================

This list is not exhaustive at present. See role internals for further
details.

.. code-block:: yaml

    # Prometheus program name
    prometheus_program_name: "prometheus"

    # Prometheus full version
    prometheus_full_version: "prometheus-1.1.2.linux-amd64"

    # Prometheus version tag for upstream sources
    prometheus_version: "v1.1.2"

    # Prometheus etc directory variable
    prometheus_etc_directory: /etc/prometheus

    # Prometheus system user
    prometheus_system_user_name: prometheus

    # Prometheus system group
    prometheus_system_group_name: prometheus

    # Prometheus extra config parameters
    prometheus_program_options: "-config.file=/etc/prometheus/prometheus.yml -alertmanager.url http://localhost:9093"

    # Prometheus data directory
    prometheus_data_directory: "/data"


Additional Variables
====================

Alert Manager is a seperate daemon that listens on port 9093 by default.

This list is not exhaustive at present. See role internals for further
details.

.. code-block:: yaml

    # Enable alertmanager
    alertmanager_enabled: true

    # Alert Manager port
    alertmanager_port: 9093

    # Alert Manager program name
    alertmanager_program_name: "alertmanager"

    # Alert Manager full version name
    alertmanager_full_version: "alertmanager-0.4.2.linux-amd64"

    # Alert Manager version tag for upstream
    alertmanager_version: "v0.4.2"

    # Alert Manager etc directory
    alertmanager_etc_directory: /etc/alertmanager

    # Alert Manager system user
    alertmanager_system_user_name: alertmanager

    # Alert Manager system group
    alertmanager_system_group_name: alertmanager

    # Alert Manager extra config parameters
    alertmanager_program_options: "-config.file=/etc/alertmanager/alertmanager.yml"

    # Alert Manager smtp smart host
    alertmanager_smtp_smarthost: "localhost:25"

    # Alert Manager smtp source email address
    alertmanager_smtp_from: "email@test.com"

Example Playbook
================

.. code-block:: yaml

   - name: Install prometheus server
     hosts: prometheus_all
     user: root
     roles:
        - { role: "os_prometheus_server", tags: [ "os-prometheus-server" ] }
     vars:
       is_metal: "{{ properties.is_metal|default(false) }}"

Additional Notes
================

This playbook is not part of the official upstream projects and as such there
are a few extra steps in getting this role deployed. We have included an extras
directory in this repo with the required modifications needed to install this
role.
