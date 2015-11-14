---
layout: post
title: "How to change Wordpress Table Prefixes"
description: "Automation of step-by-step instructions on how to change Wordpress table prefixes using Linux tools"
category: "security"
tags: [beginner, wordpress, security, tools]
---

# Applicability of Instructions
Instructions are as of December 11th, 2013 against a Wordpress 3.7.1 instance. Must have ability for command-line
access to Wordpress database using mysql.

# Background
A family friend has been using Wordpress to host his Yoga website. The site had been repeatedly attacked by hackers who got
inside Wordpress and started hosting spam HTML pages on his site. I didn't know that much about Wordpress so we cleaned
it up repeatedly and they came back repeatedly. Finally, we really started to clamp down on security using the ever-evolving
Exsiter backup and its digital fingerprinting/md5 hashes to pinpoint changes (see [Jexsiter at Github](https://github.com/medale/JexSiter/)).

It seems we got ahead of the hackers and their botnet scripts for now so we wanted to further harden the site. One way was to
change the Wordpress database table prefixes from wp_ to something else (example here is b42_). We followed the procedures 
described in the excellent Wordpress beginner tutorial at [http://www.wpbeginner.com/wp-tutorials/how-to-change-the-wordpress-database-prefix-to-improve-security/](http://www.wpbeginner.com/wp-tutorials/how-to-change-the-wordpress-database-prefix-to-improve-security/).

Doing this on an Ubuntu box I explored and captured how to automate some of the steps for our distro/plugins and existing database.

# Using sed to create RENAME table commands

## Sample command to rename tables
    RENAME table `wp_postmeta` TO `b42_postmeta`;

## Capturing all table names

Log in to Wordpress mysql account from MySQL command line tool (see info in Wordpress wp-config.php):

    mysql -u $WORDPRESS_DB_USER -h $WORDPRESS_DB_HOST -p $WORDPRESS_DB_NAME
    Enter password:
    
From Wordpress mysql account run:

    show tables;
    
Copy output in tables.txt. That file should look something like this:

    | wp_commentmeta           |
    | wp_comments              |
    | wp_links                 |
    | wp_newsletter_users      |
    | wp_options               |
    | wp_postmeta              |
    | wp_posts                 |
    | wp_social_links          |
    | wp_term_relationships    |
    | wp_term_taxonomy         |
    | wp_terms                 |
    | wp_usermeta              |
    | wp_users                 |

## Convert tables.txt to rename.sql statements using sed

Using sed with regex with nested group we can then generate the rename statements using sed extended regular expression syntax with nested groups:

    sed -r 's/[|] (wp_([A-Za-z_]*))[ ]*[|]/RENAME table `\1` TO `b42_\2`;/g' < tables.txt > rename.sql
   
## Now run rename.sql command against our Wordpress database

Note: Specifics of your Wordpress database connection can be found in your wp-config.php file.

    mysql -u $WORDPRESS_DB_USER -h $WORDPRESS_DB_HOST -p $WORDPRESS_DB_NAME < rename.sql

## Double-check successful execution by logging into Wordpress database via MySQL command line tool

After running this command check on database tables to ensure they have the new b42_ prefix

    mysql -u $WORDPRESS_DB_USER -h $WORDPRESS_DB_HOST -p $WORDPRESS_DB_NAME
    Enter password: 
    
    show tables;
    
Output should be

    | b42_commentmeta           |
    ...
 
## Edit Wordpress wp-config.php file
$table_prefix  = 'b42_';

## Edit database table content for b42_options and b42_usermeta tables

After making those table prefix changes you cannot log in to the Wordpress via wp-login.php due to insufficient permissions
and would probably see the following when trying:
   
    You do not have sufficient permissions to access this page
   
This is due to security pointing to the old wp_ table prefixes and we need to change that in the database itself. For us
(given our plugins - again see the [wpbeginner.com change database prefix instructions](http://www.wpbeginner.com/wp-tutorials/how-to-change-the-wordpress-database-prefix-to-improve-security/) for details - that meant the following
changes). Also see [Wordpress Support on insufficient permissions](http://wordpress.org/support/topic/wp-admin-you-do-not-have-sufficient-permissions-to-access-this-page) for exact entries.

### Log in to Mysql command line

    mysql -u $WORDPRESS_DB_USER -h $WORDPRESS_DB_HOST -p $WORDPRESS_DB_NAME

### Change b42_options table

    update b42_options set option_name = 'b42_user_roles' where `option_name` = 'wp_user_roles';

### Change b42_usermeta table

Note: With multiple accounts for Wordpress you might have multiple rows of the entries below. The update statements will fix all rows.

    update bikramyoga.b42_usermeta set meta_key = 'b42_capabilities' where meta_key = 'wp_capabilities';
    update bikramyoga.b42_usermeta set meta_key = 'b42_user_level' where meta_key = 'wp_user_level';
    update bikramyoga.b42_usermeta set meta_key = 'b42_user-settings' where meta_key = 'wp_user-settings';
    update bikramyoga.b42_usermeta set meta_key = 'b42_user-settings-time' where meta_key = 'wp_user-settings-time';
    update bikramyoga.b42_usermeta set meta_key = 'b42_dashboard_quick_press_last_post_id' where meta_key = 'wp_dashboard_quick_press_last_post_id';
    
### Log in to ensure everything works
Once all the changes above are made. Log in via web to your Wordpress Admin console and test your site by viewing your Wordpress pages!
If not, maybe you have some extra plugins? Re-read:
* [http://www.wpbeginner.com/wp-tutorials/how-to-change-the-wordpress-database-prefix-to-improve-security/](http://www.wpbeginner.com/wp-tutorials/how-to-change-the-wordpress-database-prefix-to-improve-security/)
* [http://wordpress.org/support/topic/wp-admin-you-do-not-have-sufficient-permissions-to-access-this-page](http://wordpress.org/support/topic/wp-admin-you-do-not-have-sufficient-permissions-to-access-this-page)
