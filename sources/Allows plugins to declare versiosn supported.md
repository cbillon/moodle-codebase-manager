# Allow plugins to declare which major stable versions of moodle are supported

[ici](https://tracker.moodle.org/browse/MDL-59562)

The version.php file has a way to declare which first major stable version is supported via:

$plugin->requires = '2014010101';

There are two problems with this:

1) There is no possible way to declare that a particular stable is not supported. In particular when  API's are deprecated, in the plugin we need to have multiple branches which each declare exactly what major stables they support., and don't support.

2) it's opaque and difficult to often match the date back to a stable version at a glance (admittedly a minor issue)

What I'm suggesting is a new way of declaring support like this:

$plugin->supports = array('2.9', '3.0', '3.1');

The intent of this is to declare what is known to work, which may not necessarily be exhaustive and could be out of date when new sables arrive but still actually work.

There could be a second array which explicitly declares what is known to not be supported too:

$plugin->unsupported = array('3.2', '3.3');

This data would be leveraged in a couple ways:

    If 'supported' is provided AND the current version is not in the list, then at install / upgrade time a warning would be produced.
    If 'unsupported' is provided AND the current version is in the list, or a lower value is, then this should be a hard install / upgrade failure. We can safely assume that if say 3.3 is not supported then all future versions after 3.4+ are also not supported. This value could just be the first unsupported version string, and not an array, as they are functionally identical.
    In the Moodle plugin directory this info can be parsed out and use to automatically populate the plugin metadata. The plugin directory could be configured to ingest multiple git branches from github which each declare different support levels.

[official documentation](https://moodledev.io/docs/5.2/apis/commonfiles/version.php)