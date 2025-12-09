
# Automated Plugin maintenance

[source](https://docs.moodle.org/dev/Automatic_updates_deployment)

## moosh
Moosh is a command-line tool for moodle that has a function to install/update plugins by their short name. Check their available commadns here(https://moosh-online.com/commands/). You will need to use a combination of the plugins "plugin-list" and "plugin-install -d" (-d flag is used to reinstall/update plugins that already are installed)

## Sergio Rabellino

I'm a plugin developer and a sysadmin of many Moodle instances: actually, but things are likely to change in the future, the plugin management does not have any enforcement that could simplify their management further. Someone uses the "current" distribution via the zip, others update their git repository but with tags not perfectly aligned with the Moodle naming (e.g. MOODLE_501_STABLE), so it's up to you to understand what each plugin developer is doing. Sometimes there is a new zip, but no updates on the corresponding git too...

To better standardise, my suggestion is to create an intermediate repository for each plugin you would like to use, connect the official git as upstream, and pull from your Dockerfile using your standard for tags/branches. So a sort of man-in-the-middle. This also allows putting in production temporary changes (bugfixing) without waiting for global changes.

## Petr Skoda

Hi, I've been doing a similar thing for more than 10 years now. The fetching of new versions is just a first step. The next problem will be setting up CI to run full suite of PHPUnit + Behat + upgrade tests.

From my experience the best way to create all-in-one git repository is to use git subtrees. I would never ever again use git submodules for anything. Committing everything into one regular repository is very problematic for version upgrades.

Sooner or later you will start hitting problems with upstream bug fixes, so in the end you will likely create own forked repositories with additional patches. It is beneficial to have some developer tool that clones all necessary repos for development/testing use.

Here is what I do:

- create forks of all additional plugins
- invent some json file that lists all plugin for each Moodle branch
- create developer tool that clones all additional plugins into Moodle checkout
- set up a CI that runs full PHPUnit and Behat for all plugins; add new upgrade tests using backups of sample data
- invent some tagging/branching scheme for your forked additional plugin repos
- create a subtree build tool that uses the json file and your tagging scheme to produce production all-in-on branch
- create a new tool to diff/fetch/pull upstream updates

## Howard Miller
I would caution you to consider whether it's a good idea to update plugins outside of a testing environment. They do have bugs and, occasionally, ones bad enough to bring your site offline.

## Rick Jerz
I am not a big plugin user, but with the few that I do use, I have had times where the latest release had bugs, which I found by installing them first on a test site, and therefore continued using an older release. So I avoid any automatic method of updating plugins.

A while ago, I used to always manually install plugins to a temporary, fresh version of Moodle (on a test site) before upgrading.