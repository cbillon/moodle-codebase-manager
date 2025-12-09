# Git plugin Guillaume Allegre

[ici](https://moodle.org/plugins/view.php?id=1963)

gitplugins is a very light (single file) administration tool to help deploying Moodle plugins via Git.

You need to install one single file in the /admin/cli/ directory, the gitplugins.php script.
The gitplugins.conf file is a list of all the plugins you want to manage (install, upgrade...) with the format:

```
 local/mailtest' => [
        'path' => '/local/mailtest', // mandatory ; path from the moodle root
        'gitrepository' => 'https://github.com/michael-milette /moodle-local_mailtest', // mandatory
        'gitbranch' => '', // optional ; git branch (incompatible with gitrevision)
        'gitrevision' => '', // optional ; precise git revision (hash or tag)  (incompatible with gitbranch)
    ],

```

You can then launch php gitplugins.php with one of the options:

--gen-config generates a sample gitplugins.conf file
--check checks the consistency of 'gitplugins.conf'
--diag displays a diagnostic of all declared plugins
--status launches a git status on each declared plugin
--install installs all plugins that are not already present (git clone)
--upgrade upgrades all plugins already installed (git fetch + git checkout)
--cleanup "removes" all plugins in an inconsistent state (by renaming them, so restoration is possible)
--gen-exclude generates a chunk of lines to insert in your .git/info/exclude file
"Cleaned" repositories are renamed to <orig-name>.back-<timestam>, so you can easily find and restore them if needed.

