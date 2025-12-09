## Guide line for plugin version

[ici](https://moodle.org/mod/forum/discuss.php?d=396152)

What if a new version of Moodle comes out, and we confirm that the theme is compatible with the new version without needing any changes?

**Michael Millette**

If your plugin published on Moodle.org is compatible with a newer version if Moodle without any changes, just edit your submission and add the new version of Moodle to it without uploading a new version. Some of my plugins have not required any changes since several versions of Moodle and this is what I do.

The problem with indicating exact version compatibility in version.php is that not every maintainer will keep their plugins up to date yet there is a good chance that it will work just fine in subsequent releases of Moodle.

Another option I have seen some maintainers use is to create a new branch of their plugin for each release of Moodle. Personally I would only do this if there was such a big change to my code that I did not want to have to maintain backwards compatibility.

If you really want to update your plugin to reflect compatibility with a newer version of Moodle without making changes to your code, update the documentation or the copyright notice and then submit that as a new release without changing the version number so that it doesn't unnecessarily trigger plugin updates for everyone currently using it.

**Paul Holden**

Assuming you are using Travis to automate testing of your plugins, you would at the very least want to add the new Moodle version branch to your testing matrix 🙂

Once tests pass on the new version, you can tag the release and publish to the plugins repository.


**David Mudrack**

Good questions, thanks Ray for starting the thread.

I personally tried various versioning and release naming schemes in my plugins. I have not found a nice & working solution for having the list of supported Moodle versions reflected in the plugin's version number. What finally seems to work best for me is to have my own version sequence without a numerical dependency on the Moodle version number, and mention the relation to the Moodle version in the release notes, version.php and the plugin description.

Additionally I try to adapt the ideas and spirit of the semantic versioning. When the list of supported Moodle versions change (typically I drop support for older Moodle versions), I release a new plugin version with the higher major version number etc. That way, one major plugin version supports a range of Moodle core versions. And I do breaks only for good enough reasons (e.g. Moodle 3.8 is a good candidate due to its new options of handling the JS modules).

 Also wanted to point to just recently added [MDL-59562](https://tracker.moodle.org/browse/MDL-59562) - ability for plugins to declare which major stable versions of moodle are supported directly in their version.php file (supported since Moodle 3.9)

[Improved validations API for mainteners ability to release by tagging at github](https://moodle.org/mod/forum/discuss.php?d=423251#p1705237)
[plugin ci Moodle HQ](https://github.com/moodlehq/moodle-plugin-release)

[Other thread](https://moodle.org/mod/forum/discuss.php?d=264988)
[version.php ](https://moodledev.io/docs/5.1/apis/commonfiles/version.php) documentation officielle

**Tim Hunt**

I am with Marcus. Trying to make your version numbers correspond to Moodle version numbers seems appealing at first, but there are too many things that might force them out of sync, and they you are left with version numbers that look a bit like Moodle version nubmers, but actually don't match.

So, I now number my plugin releases v1.0, v1.1, ... Those are the tag names I use in git. If I need different versions of my plugin to work with different Moodle branches, I will make tags like v1.1_m21, v1.1_m22

Then, in the version.php file, I put a fuller description like

$plugin->release   = '1.3 for Moodle 2.5+';

**Joseph Reseau**
**I think for end-users it's clearer for plugins to have the same major version number as the Moodle versions. And that's what I do with the plugins I maintain.**


**David Mudrak**

Its primary purpose is to enable multiple branches of the plugin, as Davo noted. Some add-on maintainers follow the Moodle core's development model and they have branches like master, MOODLE_26_STABLE, MOODLE_25_STABLE etc in their add-on. Imagine there is a plugin FooBar version 5.0 released for Moodle 2.5.x series, and also FooBar version 6.0 for Moodle 2.6.x series (the maintainer of the plugin has them on separate branches). Let us say that there was some fix needed in a code specific to the 5.0 version so the maintainer wants to release the version 5.1 of the plugin (for Moodle 2.5.x).

The problem is, the plugin's version must never get "disordered". That means, the version number of 5.0 must be always lower than 6.0. But also, any (future) 5.x version of the plugin must be lower than any 6.x version.

If the maintainer did a mistake and had, for example

$plugin->version = 2014010100;  // For the plugin release 5.0
$plugin->version = 2014010101;  // For the plugin release 6.0

and then in the new release 5.1 would do something like

$plugin->version = 2014032400;  // For the plugin release 5.1

then poor users will not be able to upgrade the plugin from 5.1 to 6.0 (as Moodle would consider it as a downgrade from 2014032400 to 2014010101).

The solution is to do what Moodle core does. Freeze the date-part of the version number once a new stable branch of the plugin is released and use the "xx" as the incremental counter for the updates on that branch. So the correct situation would look like this:

$plugin->version = 2014010100;  // 5.0
$plugin->version = 2014010200;  // 6.0
$plugin->version = 2014010101;  // 5.1

If you do not use multiple stable branches in your plugin and all the releases are made off a single (master) branch in a linear way, then using the date of the release will guarantee the upgrade doable, of course.

Just a side note, the Moodle core uses decimal numbers in the main version so it has more than 100 ugrade steps available on stable branches. Plugins still has this limit, but it is not a big deal. If 100 upgrade steps is not enough for a single plugin, one should not consider that branch "stable" anyway

Howard Miller
If a plugin works for Moodle 5.something then it should work for Moodle 5.anything. HQ promise not to let through any breaking changes.

Leon Stringer
It's certainly annoying. The latest [mod_scormremote](https://moodle.org/plugins/mod_scormremote/versions) (version 2024100300 released 3 weeks ago) is listed as compatible with Moodle 3.9 to 4.4 but has code which only works with 3.11 onwards.