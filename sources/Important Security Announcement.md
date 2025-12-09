
## Important Security Announcement
par Michael Hawkins, mercredi 20 août 2025, 10:00

[MSA](https://moodle.org/security/index.php?o=3&s=10&p=1)

Hello Moodlers,

We have become aware of an increase in malicious activity directed towards Moodle instances globally and are writing to inform you of the situation, along with some guidance on steps you can take to protect your system. This malicious activity is external in nature rather than through Moodle itself.   

What’s going on? 

It has been observed across several Moodle hosting partners and self-hosted sites that a large number of authentication attempts are being made to a rarely used administration page.  These attempts are likely coming from a malicious botnet that is using a large database of compromised credentials - which are typically obtained through data breaches across the web - to test if they have been reused on Moodle admin accounts.  

This is not an unusual event, but the volume has been far higher than observed in the past and indicates there may be an elevated risk.

In this particular instance, from the page being accessed, there are indications that the botnet is attempting to install a plugin for its own purposes.  However, this may not be the only activity that is being undertaken.

The specific attack being observed targets sites using manual Moodle authentication. We do not believe it impacts users using SSO integrations for their login, however the recommended steps below will be prudent for all Moodle systems.

It is important to note that the source of the credentials being exploited is not believed to be from any system associated with Moodle HQ or our Moodle Certified Partners and Service Providers.

Is this a vulnerability in Moodle itself?

No, this is not a vulnerability in Moodle or its code.  This is a result of a large number of user credentials that have been made available via one or more data breaches. This is a problem that is common to all systems that require authentication on the internet.  Any password reuse can put all systems that share that password at risk.

What can you do to protect your system? 

We recommend that you take immediate action on several fronts to protect your Moodle installations.

Change the password on all your admin accounts immediately - this will ensure any stolen credentials that have been reused will no longer work.  Consider also resetting passwords for other users as well.  Passwords should always be unique and complex to remain secure. You can enforce password complexity in the admin settings.  Documentation to do so can be found HERE. 

Consider implementing multi-factor authentication (“MFA”), particularly for admin accounts -  MFA will help prevent any such attempts to access the system even if the credentials are successful, as the user will be asked to authenticate using email, phone or other means.  Moodle has supported MFA natively since the release of Moodle 4.3, and related documentation can be found HERE.  If you are using a version of Moodle that is older than 4.3, consider upgrading so you can use MFA.  Alternatively, your version may be supported by the Catalyst IT Multi-factor authentication plugin.

Disable web-based plugin installs - If you self host your Moodle site, and want to ensure that someone with a working admin credential to your site cannot enable or install a malicious plugin, you can disable the web-based plugin installer by adding this to your site’s config.php file:

$CFG->disableupdateautodeploy = true;

If you do not have command line access to your site’s config.php please contact your hosting provider for assistance.

If I self host Moodle, how can I detect if my site is being targeted?

The easiest way to detect these attacks is to search your web logs for attempts to access the path /admin/tool/installaddon/index.php. This is the page the attacker is attempting to access. It is very rarely, if ever, used on a production site, so any attempts to access it should be researched closely.

If your Moodle implementation is provided to you via MoodleCloud Standard or Premium hosting services, rest assured that every precaution is being taken to mitigate this risk. 

However, this type of malicious activity is commonplace across the internet, and good password practices rely on your support, so please make sure to apply the recommended protection measures for password management. 

We will continue to monitor this situation and inform the community as we become aware of more information.

Thank you for your attention to this matter and happy Moodling.

The Moodle HQ Team