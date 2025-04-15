

[API plugin directory](https://moodledev.io/general/community/plugincontribution/pluginsdirectory/api)

## GitHub Actions

A new workflow can be configured at GitHub Actions to automatically release a new version in the Plugins directory once a tag is pushed to the repository. Please see [ici](https://github.com/moodlehq/moodle-plugin-release) for details.

## Tips

Use settings $plugin->requires, $plugin->supported and $plugin->incompatible in your plugin's version.php. 
They are used to automatically populate the list of supported Moodle versions. 
By default, all Moodle versions starting from the one described by $plugin->requires will be marked as supported.

note $plugin->requires fait référence à une version Moodle mais il est risqué de présumer du fonctionnement dans les versions ultérieures (cas de changements d'API)
$plugin->supported déclare explicitement les versions supoortés on indique le XXX de la branche stable de la version de Moodle MOODLE_XXX_STABLE

Recommendation Moodle aux dev

Supported Moodle versions

    New plugins submitted into the plugins directory must support at least one of the currently maintained Moodle version.

Code repository name

    Provide a consistent experience for other Moodle developers and site administrators - follow the repository naming convention for Moodle plugins: moodle-{plugintype}_{pluginname}.

Source control URL

    Facilitate sharing and further development of your open-source plugin - provide publicly accessible URL of your code repository.
    Github is a choice of most Moodle plugin developers.
