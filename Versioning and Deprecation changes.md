# Versioning and Deprecation changes

[site](https://moodle.org/mod/forum/discuss.php?d=457946)
Matt Porritt  lundi 29 Avril

Currently, the first two numbers for a version represent the major version, and the third number represents the minor version. There haven’t been set rules as to when the first number is increased, and since Moodle 2.0 there has not been any special meaning to it. The changes to this number for 3.0 and 4.0 were somewhat linked to major underlying changes in LMS, but the size of this change itself was variable. This unpredictability makes it challenging for administrators and developers to understand what an increase in version number means.

To address this we are making the change to add more meaning to version numbers, starting from version 4.5 LTS. The changes are:

    - The first part of the version will now represent a Series
    - The last release in each Series will be an LTS release
    - The next major release after an LTS will mark the beginning of a new Series

This is how this will look over the next few releases:

    Series 4:
        4.1 Current LTS (released)
        4.2 Past release (released)
        4.3 Past release (released)
        4.4 Current release (released)
        4.5 Next LTS release - This is the last release in the 4.x series. (Release: 7th October, 2024)
    Series 5:
        5.0 Standard release (Release: 21st April, 2025)
        5.1 Standard release  
        5.2 Standard release
        5.3 LTS release - This is the last release in the 5.x series.
    Series 6:
        6.0 Standard release
        6.1 Standard release
        6.2 Standard release 
        6.3 LTS release - This is the last release in the 6.x series.

Streamlined Deprecation Process

Starting from LMS version 4.5 We are also updating the deprecation policy for Moodle LMS to align more closely with the LTS cycle. The changes are:

    Deprecations will now be aligned with the LTS release cycle, providing a clear timeline for when  deprecated features need to be updated or removed.
    Features deprecated before an LTS release will be removed in the release following that LTS. 

This adjustment means the shortest deprecation period will be 12 months, down from the previous 24 months. Features that have been deprecated in LMS version 4.3 or 4.4 will be affected by this new approach; they will be removed in 5.0, which is the version after the 4.5 LTS.

These changes aim to foster a more consistent support cycle, benefiting both Moodle core development and plugin developers. It encourages a single plugin branch per LTS series, reducing the complexity of supporting multiple Moodle versions.

Dan Marsden répond à :
Hi Visvanath, 

One of the challenges your proposal above doesn't solve is that people often use submodules to add plugins to their codebase, and sometimes will automate processes to pull in new changes.

In particular this statement you made:
"Moodle 5.0 will be released. Now you have to make a branch for the Moodle 4 series. The head will be for Moodle 5.x, initially corrected for version 5.0."

means that someone using a Moodle 4.x branch pointing at "main" with automation - will pull in a change that suddenly breaks their site and they will have to do work on their end to fix the branches used in their submodule checkout.

**What we do here at Catalyst with most of our plugins is that we don't use a branch named "main" at all, the latest branch name will be named after the earliest Moodle branch it supports.**

example:

Saml2 has a current "latest" branch name called "MOODLE_39_STABLE" - this supports all versions since MOODLE_39_STABLE

If something in Moodle 5.0 means we have to create a new branch - we call that new branch MOODLE_500_STABLE and then when something after that means we need a new branch, we create MOODLE_600_STABLE etc.

This means if a Moodle 4.1 site using submodules linking to MOODLE_39_STABLE still functions correctly and you don't need to change the branch it's currently using.


***So my question is, can't HQ impose a versioning concept for additional plug-ins if they were to be included in the official plug-in database? Or, am I naive?***

The simple answer is, that Moodle does enforce a versioning concept on plugins - it's built-in to the Moodle plugins directory.

If you pull the data from there, you get a list of which released version of each plugin is suitable for any given version of Moodle, along with a link to download it (there's a 7MB JSON file you can pull down with everything in it - that's what our company's internal tools use for managing 3rd-party plugins).

Some plugins may support and encourage people to download them from github, in which case feel free to do so.

I can state, for example, that none of my own plugins offer stable versions in github - you can download from there if you want, but the stable, supported versions are in the Plugins directory. There is no need for me, as a plugin developer, to conform to any particular branching scheme, because github is just the place where the current development code is kept for the plugin.


note : 

introduit le concept de serie, la version LTS étant la derniere de la série
       pas de changement le 2 premiers caracteres indiquent une version majeure 

       **A une version majeure correspond une branche MOODLE_XXX_STABLE**
depreciation : 
- annoncer dans chaque version de la série
- effecfective dans la prochaine version apres la LTS pour les dépréciations annoncées avant la LTS 

**One big advantage that might not be clear is that if a 3rd party plugin works in 5.0 it should also work fine in 5.3, but then may break in 6.0 - we also like the last release in the series being the LTS version too.** 
As a plugin developer, this affects me because, while I will hopefully be able to limit my number of branches to one per series

Préconisation ; pour chque plugin avoir une branche correspondant à la série supportée
