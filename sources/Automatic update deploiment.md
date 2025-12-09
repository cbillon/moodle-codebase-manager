## Automatic deploiement

[source](https://docs.moodle.org/dev/Automatic_updates_deployment)

### Enabling updates deployment
This functionality requires Available update notifications to be enabled. The feature is enabled by default as long as the web server has write access to the folders with plugins being updated.

### Disabling updates deployment
In a few circumstances (such as completely managed servers, which may have a lot of local modifications, or sites that have their own solution for updates deployment - for example via Git checkouts) it is desirable to not to allow automatic updates deployment. The feature may be disabled completely by adding the following code to the config.php file:

// Use the following flag to completely disable the installation of plugins
// (new plugins, available updates and missing dependencies) and related
// features (such as cancelling the plugin installation or upgrade) via the
// server administration web interface.

  **$CFG->disableupdateautodeploy = true;**