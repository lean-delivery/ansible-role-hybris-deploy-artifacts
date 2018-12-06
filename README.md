Hybris deploy artifacts
=========

Role for deployment of Hybris artifacts to configured Hybris instance using hybris preinstall utility (h-up).
H-up utility could be installed by lean_delivery.hybris_bootstrap_node role.

Role tasks
------------

  - Deploy artifacts to server using h-up
  - Initialize or update DB using h-up
  - Start Hybris server


Keep in mind
------------

We have used ENV Hack in playbook:

environment:
  LC_ALL: "en_US.UTF-8" # only for Docker

Requirements
------------

  - Minimal Version of the ansible for installation: 2.5
  - Java 8 [![Build Status](https://travis-ci.org/lean-delivery/ansible-role-java.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-java)
  - hybris_bootstrap_node [![Build Status](https://travis-ci.org/lean-delivery/ansible-role-hybris-bootstrap-node.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-hybris-bootstrap-node)
  - Supported OS:
  - CentOS
    - 7

Role Variables
--------------

  - `htools.hybris_tools_path` - path to htools dir
    default: "/opt/hybris-tools"

  - `hda_hup_extra_opts` - option to include initialize or other option from h-up
    default: ""
  - `hda_hybris_http_host` - hybris host
    default: "localhost"
  - `hda_hybris_https_port` - hybris https port
    default: "9002"
  - `hda_hybris_check_url` - hybris admin login page
    default: "login.jsp"
  - `hda_hybris_service_name` - hybris service name
    default: "hybrisd"

  - `hda_artifacts_deploy_version` - hybris artifacts version
    default: "dev/1"

  - `hda_hybris_start` - to start hybris after artifacts deploy
    default: "False"
  - `hda_hybris_artifacts_timeout` - timout for artifacts deploy in minutes
    default: "60"
  - `hda_hybris_artifacts_delay` - delay for artifacts deploy in seconds
    default: "30"

  - `hda_hybris_service_timeout` - timeout for checking the availability of hybris service in minutes
    default: "30"
  - `hda_hybris_service_delay` - delay for checking the availability of hybris service in seconds
    default: "5"

  - `hda_debug_mode` - enable writing deploy log to controller {date}-{instance}.log
    default: "False"
  - `hda_debug_directory` - save debug file to this directory
    default: "/tmp"

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- name: "Converge"
  hosts: all
  vars:
    htools.artifact_storage: "http://server/hybrisArtifacts"
    artifacts_deploy_version: "latestArtifacts/hybrisServer"
    hda_hup_extra_opts: "--initialize"
  roles:
    - role: lean_delivery.java
    - role: lean_delivery.hybris_bootstrap_node
    - role: lean_delivery.hybris_deploy_artifacts
```

License
-------
Apache


Author Information
------------------

authors:
  - Lean Delivery Team <team@lean-delivery.com>
