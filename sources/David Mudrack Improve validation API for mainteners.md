Improved validation, API for maintainers and ability to release by tagging at GitHub
par David Mudrák, mercredi 9 juin 2021, 22:53

Hello! I am very happy to finally announce availability of some new features in the Moodle Plugins directory. These improvements are mostly relevant for the maintainers who release new versions of their plugins regularly.

Improved version number validation
Plugins must have well formatted version number defined as $plugin->version in their version.php file. Invalid values used to raise warning only before.
If specified, the $plugin->requires must be Moodle core version number in the form of YYYYMMDDRR or YYYYMMDDRR.XX. Invalid values did not raise any warning before.
For plugins that specify $plugin->requires only in their version.php, all Moodle releases with version number equal or greater than the required one will be automatically selected as supported by default.
The incompatible Moodle branch specified in $plugin->incompatible is now validated and taken into account when populating the default list of supported Moodle versions (all between the required one and the incompatible one).
Supported Moodle branches specified in $plugin->supported are now respected when populating the list of supported Moodle versions. Only versions that pass all present conditions (supported, requires and incompatible) will be selected.
It is no longer possible to release a new version that would have the same version build number as some already released version. This is intended to avoid having different ZIP packages both appearing as the same version which effectively breaks other mechanisms in Moodle such as available update notifications.
When attempting to release a new version that has the version number lower than some other already existing plugin version supporting the same Moodle version, a validation warning is raised. Without further action (such as hiding the version that had existed), the newly added version would have no effect on Moodle branches supported by both plugin versions.
API for maintainers
Plugins directory has some of its functionality exposed via web service now. This allows maintainers to release new versions of their plugins automatically - for example using local shell scripts - without the need to fill the form at the web UI.

Please see Plugins directory API docs page for details.

Release by tagging at GitHub
The new API allows to implement integrations with your CI and release workflows. An example of such an integration - ability to release new plugin versions simply by tagging them at GitHub - has been published. Please see https://github.com/moodlehq/moodle-plugin-release for details.

Many thanks everybody for your valuable inputs and suggestions in relevant tracker issues MDLSITE-4781 and MDLSITE-4041.

Note David Mudrack
A new version of the workflow template was published today with a few improvements including the authentication security concerns. The new workflow no longer needs moodle.org username and password stored anywhere. Instead, developers are expected to generate the token directly via the web interface in the plugins directory and use it instead. This token has the scope limited to this particular service only and is therefore much safer to be worked with.

For the full list of improvements, see the CHANGES.md file at https://github.com/moodlehq/moodle-plugin-release