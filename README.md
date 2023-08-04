Ansible Role: node\_exporter
==========================

[![Build Status](https://travis-ci.org/atosatto/ansible-bind_exporter.svg?branch=master)](https://travis-ci.org/atosatto/ansible-bind_exporter)
[![Galaxy](https://img.shields.io/badge/galaxy-atosatto.bind_exporter-blue.svg?style=flat-square)](https://galaxy.ansible.com/atosatto/bind_exporter)

Install and configure Prometheus node\_exporter.

Requirements
------------

An Ansible 2.2 or higher installation.<br />
This role makes use of the Ansible `json_filter` that requires `jmespath` to be installed on the Ansible machine.
See the `requirements.txt` file for further details on the specific version of `jmespath` required by the role.

Role Variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml):

    bind_exporter_release_tag: "latest"

The node\_exporter release to be installed.
By default, the latest release published at https://github.com/prometheus/node\_exporter/releases.

    bind_exporter_release_url: ""

If set, the role will download bind-exporter from the provided URL instead of using the download URL indicated in the node\_exporter Github release metadata.

    bind_exporter_user: "bind_exporter"
    bind_exporter_group: "bind_exporter"

node\_exporter system user and group.

    bind_exporter_install_path: "/opt"

Directory containing the downloaded node\_exporter release artifacts.

    bind_exporter_bin_path: "/usr/local/bin"

Directory to which the node\_exporter binaries will be symlinked.

    bind_exporter_listen_address: "127.0.0.1:9100"

The node\_exporter WebServer listen ip address and port.<br/>
**NOTE**: the node\_exporter metrics will be available at `{{ bind_exporter_listen_address }}/metrics`.

    bind_exporter_log_level: "info"

node\_exporter logs verbosity level.

    bind_exporter_collector_textfile_path: "/var/lib/bind_exporter/textfile-collector/"

Directory used by the node\_exporter's textfile collector to look for `*.prom` metrics files to be
exposed by the exporter.
See https://github.com/prometheus/bind_exporter#textfile-collector.

    bind_exporter_additional_cli_args: ""

Additional command-line arguments to be added to the node\_exporter service unit.
For the complete refence of the available CLI arguments please refer to the output
of the `bind_exporter --help` command.

Dependencies
------------

None.

Example Playbooks
-----------------

    $ cat playbook.yml
    - name: "Install and configure Prometheus bind_exporter"
      hosts: all
      roles:
        - { role: atosatto.bind_exporter }

Testing
-------

Tests are automated with [Molecule](http://molecule.readthedocs.org/en/latest/).

    $ pip install tox

To test all the scenarios run

    $ tox

To run a custom molecule command

    $ tox -e py27-ansible29 -- molecule test -s bind_exporter-latest

License
-------

MIT

Author Information
------------------

Andrea Tosatto ([@\_hilbert\_](https://twitter.com/_hilbert_))
