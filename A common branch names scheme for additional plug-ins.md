# A common branch names scheme for additional plug-ins ?

[ici](https://moodle.org/mod/forum/discuss.php?d=454264)

Andrew Lyons
From my experience, the vast majority of plugins have a single branch, and attempt to support all current versions of Moodle with a single plugin version.

Personally I'd like to see that change a little with one branch per set of releases 

Developers of plugins do have to get their submission vetted and approved for listing in Moodle's plugins site.   But from what I've read in the past, plugins are not checked ever again.   It is up to developer of the plugin to maintain.   Think they also have enough access to moodle HQ's plugin site to upload their latest versions.

Davo Smith

 think the fundamental question here is why you are trying to pull code from github, not from the Moodle plugins directory.

Github usually contains the latest "in development" code, the code in the Moodle Plugins directory is the version that has been published and declared stable.

You might be better off with the process that some of our internal scripts use, that downloads the data from: https://download.moodle.org/api/1.3/pluglist.php then uses the relevant download URL in that to get the zip file of the plugin in question. After that, it's just case of deleting the existing directory, unzipping the new version of the plugin into that location, then committing the update.

Davo Smith
 I'm just pointing out that the code in github is often 'work in progress' code, that may not be fully tested or ready for use in production.

The normal source of plugins that are ready to install on production sites is the Moodle plugins directory.

I'm also not suggesting you write individual git commands or manually install anything, I'm simply suggesting an automated script that pulls plugins from the Moodle plugins directory (gathering the details from the JSON file at the URL I already posted), then adding them to your git repo. Run the script, it fetches everything and commits it to your git repo - it should work for all existing sites and doesn't require any change in process for the deployment of your sites (assuming you are just deploying the branches from your repo for those sites).

As I said above, I know this process can be automated, because it's the main principal behind an internal script we've used to do something similar ourselves (but which also handles a lot of other internal processes, so not suitable to be shared).

The only missing part is clear instructions on how to set up and name the Git branches.

**Now that the "set of releases", newly called series, is getting formalized in the core, what remains it to request the plug-in developers to open a branch per series**