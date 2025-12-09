Add support for routing of regular pages


https://moodle.atlassian.net/browse/MDL-82565


As a followup to the introduction of routing, we want to add support for routing other pages in Moodle.

For example, to access /course/view.php?id=2 to access a course with id of 2, it would be ideal to have a URL such as /course/view/2 or /course/view/name:shortname.

These ability to support this kind of notation is introduced by MDL-81031: Initial implementation of the Routing system
Closed
 but no routes currently apply to standard pages.

As part of this we would also want to look at a b/c shim, for example to redirect to the new location.

Testing Instructions

Configure the router per the instructions at https://docs.moodle.org/405/en/Configuring_the_Router

Configuring Apache2

Configuring Moodle

Restart Apache or php-fpm as required

Edit lib/templates/full_header.mustache to add the following straight after the the core/welcome inclusion:



{{#settingsmenu}}
                    <div class="me-auto">
                        {{{settingsmenu}}}
                    </div>
                {{/settingsmenu}}
Navigate to your site

Log in

Navigate to a course

You will see a weird dropdown just before "Bulk Actions" - > Open it slightly smiling face

Mouse over the "More..." link

Confirm that the URL is /course/[courseid]/manage

Click on the "More..." link

Confirm that the page loads

Shims
As an admin, enter the URL <YOUR_SITE_URL>/course/admin.php?courseid=<course_ID> on your browser.

Confirm that you are redirected to <YOUR_SITE_URL>/course/<course_ID>/manage

Enter the URL <YOUR_SITE_URL>/course/tags.php?id=<course_ID>

Confirm that you are redirected to <YOUR_SITE_URL>/course/<course_ID>/tags

Log out and log in as a student and enter the URL <YOUR_SITE_URL>/course/tags.php?id=<course_ID>

Confirm that you get an error saying you don't have permission to change course tags.