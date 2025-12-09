
## Plugins directory API

[Plugins directory API](https://moodledev.io/general/community/plugincontribution/pluginsdirectory/api)

The API has been designed so that:

The actual ZIP can be taken from pre-uploaded file (standard way of using webservice/upload.php), or submitting the file contents directly, or providing an URL the ZIP should be fetched from.
As many as possible parameters (such as list of supported Moodle versions, release name, release notes etc) default to the values specified in the ZIP itself.
So it should be enough to specify just the plugin (either by numerical ID number of frankenstyle) and the ZIP with the new version. All other values are optional and can be used to override the auto-detected ones.

## Github Actions

A new workflow can be configured at GitHub Actions to automatically release a new version in the Plugins directory once a tag is pushed to the repository. Please see https://github.com/moodlehq/moodle-plugin-release for details.


### Releasing Moodle plugins in the Plugins directory automatically from GitHub Actions

Usage
Copy the template file moodle-release.yml into the .github/workflows/moodle-release.yml location within your plugin repository.

Edit the file and set the PLUGIN environment variable to the full component name (aka frankenstyle) of your plugin. Example:

 env:
   PLUGIN: mod_subcourse
There should be no need to edit any other line as long as you are happy with the default behaviour of the workflow. Please refer to the GitHub Actions documentation for details.

Log in to the Moodle Plugins directory at https://moodle.org/plugins/. Locate the Navigation block > Plugins > API access. Use that page to generate your personal token for the plugins_maintenance service.

Go back to your plugin repository at Github. Locate your plugin's Settings > Secrets section. Use the 'New repository secret' button to define a new repository secret to hold your access token. Use name MOODLE_ORG_TOKEN and set the value to the one you generated in previous step.

That's it! Now when you tag the repository with a tag that matches the configured condition, the tagged version will be released in the plugins directory.

Tips
Use settings $plugin->requires, $plugin->supported and $plugin->incompatible in your plugin's version.php. They are used to automatically populate the list of supported Moodle versions. By default, all Moodle versions starting from the one described by $plugin->requires will be marked as supported.

Keep the CHANGES.md file in the root of your repository. It will be automatically imported as release notes for the new version. Please see Moodle dev docs for all supported names and formats.

If your release tags do not start with v character (such as v9.0.1) and you want to trigger the workflow for any tag, change the condition in the YAML file as:

on:
  push:
    tags:
      - '*'
