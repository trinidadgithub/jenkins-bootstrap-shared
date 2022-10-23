# Migration notes Oct 2022

A lot is changing this update over prior jenkins-bootstrap-shared upgrades.
This document attempts to provide a short list of changes required of end users
if they're updating.

This update includes dependency updates because a lot has changed in upstream
Jenkins.  This update also contains terminology updates to match Jenkins
community guidelines.

- Oracle JDK 8 dropped
- Some configuration scripts have been renamed
- Settings for scripts have changed
  - configure-docker-cloud.groovy
  - configure-jenkins-settings.groovy
  - configure-yadocker-cloud.groovy

See [Git commit `0861accfb96932baf1e9bc99cbc78831d3aad8c1`][1] for a full list
of terminology changes.

[1]: https://github.com/samrocketman/jenkins-bootstrap-shared/commit/0861accfb96932baf1e9bc99cbc78831d3aad8c1

# Oracle JDK 8 dropped

Oracle JDK 8 has been completely dropped.  OpenJDK 11 is now required.  If
upgrading from older version of Jervis use the older Docker image which contains
Oracle JDK 8.  After update start with the latest Docker image because it
contains OpenJDK 11.

# Some configuration scripts have been renamed

`scripts/` directory files have been renamed.  Users will need to update
`jenkins_bootstrap.sh` to reflect the following.

    configure-job-restrictions-master.groovy -> configure-job-restrictions-controller.groovy
    security-disable-agent-master.groovy -> security-disable-agent-controller.groovy

# Settings for scripts have changed

Some configuration files have had their settings updated.

### configure-docker-cloud.groovy

Settings containing `slave` have been renamed to use `agent.

    launcher_prefix_start_slave_cmd -> launcher_prefix_start_agent_cmd
    launcher_suffix_start_slave_cmd -> launcher_suffix_start_agent_cmd

### configure-jenkins-settings.groovy

The variable used for customizing settings has changed.  In your configs change
the following.

    master_settings -> controller_settings

Settings containing `master` have been renamed to use `controller`.

    master_executors -> controller_executors
    master_labels -> controller_labels
    master_usage -> controller_usage

Settings containing `slave` have been renamed to use `agent.

    jnlp_slave_port -> jnlp_agent_port

### configure-yadocker-cloud.groovy

Settings containing `slave` have been renamed to use `agent.

    launch_ssh_prefix_start_slave_command -> launch_ssh_prefix_start_agent_command
    launch_ssh_suffix_start_slave_command -> launch_ssh_suffix_start_agent_command
    launch_jnlp_slave_jar_options -> launch_jnlp_agent_jar_options
    launch_jnlp_slave_jvm_options -> launch_jnlp_agent_jvm_options

Settings containing `master` have been renamed to use `controller`.

    launch_jnlp_different_jenkins_master_url -> launch_jnlp_different_jenkins_controller_url