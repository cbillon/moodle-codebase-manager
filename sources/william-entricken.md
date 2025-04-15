[preconisation](https://github.com/moodlehq/moodle-docker/issues/304)
I believe that every Moodle plugin project should include instructions to test their module in a live, local Moodle environment.

I also think that moodle-docker is the canonical Docker repo to use for developing and testing Moodle plugins.

This means that all the instructions at https://github.com/moodlehq/moodle-docker?tab=readme-ov-file#quick-start are incorporated into the development of every plugin.

https://github.com/moodlehq/moodle-docker/pull/249

https://github.com/fulldecent/moodle-local_plugin_template/blob/00766d33b6ac9d1c80612b0475ecff983032d692/README.md#quick-start-playground



## Coding best practices for creating open source Moodle plugins ##
par [William Entriken](https://moodle.org/mod/forum/discuss.php?d=462107), mardi 17 septembre 2024, 02:16

Hello, at our company we will be creating several Moodle plugins and I am planning to release them as open source software.

Here is one that lets you create course tokens that work like prepaid gift cards. Anybody can use them to create an account on your LMS and enroll in that course. And they expire after first use. There are a bunch of other goodies, reporting, and extensibility in there too.

I would like to ask help, please, is there any very well maintained existing plugins I can study that are managed well? Or any great resources for best practices when making plugins?

Specifically I am looking at:

 - Setting up testing
 - Automating testing with GitHub Actions
 - Linting/pretifying code to match established community conventions
 - Skeleton layout of folders/files in the repo
 - Any required features for publishing the plugin to the Moodle plugin directory
 - Best practices for supporting the new Moodle versions before they come out (e.g. GitHub Action cron job using a version matrix)


** Without these best practices you quickly get a project that is unmaintainable, works for you but not for other people that download it, or goes stale when a new Moodle is released.**

So I find it valuable to iron out these details first and document them, and publish a MVP "best practices demo" plugin before seriously releasing my real projects.