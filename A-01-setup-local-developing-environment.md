## prepare Mariadb container and setup database schema

* export wordpress database

![wp-db-export-01](images/wp-db-export-01.png)

* prepare wordpress mariadb 
* prepare wordpress web
* prepare wordpress:cli 

## wordpress cli usage
```
docker-compose up -d --build

[fli@192-168-1-4 easy-wordpress-docker]$ docker container ls
CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
82e551b07076        wordpress-cli                  "docker-entrypoint.s…"   20 seconds ago      Up 19 seconds                                wordpress-cli
27c6034692ae        wordpress-web                  "docker-php-entrypoi…"   23 seconds ago      Up 20 seconds       0.0.0.0:8081->80/tcp     wordpress-web
5864c035898a        phpmyadmin/phpmyadmin:latest   "/docker-entrypoint.…"   23 seconds ago      Up 20 seconds       0.0.0.0:8080->80/tcp     phpmyadmin
eeff7f6d9646        wordpress-db                   "docker-entrypoint.s…"   24 seconds ago      Up 23 seconds       0.0.0.0:3306->3306/tcp   wordpress-db
[fli@192-168-1-4 easy-wordpress-docker]$ 

[fli@192-168-1-4 easy-wordpress-docker]$ docker exec -it 82e bash
bash-5.0$ 
bash-5.0$ which wp
/usr/local/bin/wp
bash-5.0$ wp --info
OS:     Linux 3.10.0-1062.12.1.el7.x86_64 #1 SMP Tue Feb 4 23:02:59 UTC 2020 x86_64
Shell:
PHP binary:     /usr/local/bin/php
PHP version:    7.3.17
php.ini used:
WP-CLI root dir:        phar://wp-cli.phar/vendor/wp-cli/wp-cli
WP-CLI vendor dir:      phar://wp-cli.phar/vendor
WP_CLI phar path:       /sites
WP-CLI packages dir:
WP-CLI global config:
WP-CLI project config:
WP-CLI version: 2.4.0
bash-5.0$

bash-5.0$ pwd
/sites
bash-5.0$ ls
index.php             wp-activate.php       wp-comments-post.php  wp-content            wp-links-opml.php     wp-mail.php           wp-trackback.php
license.txt           wp-admin              wp-config-sample.php  wp-cron.php           wp-load.php           wp-settings.php       xmlrpc.php
readme.html           wp-blog-header.php    wp-config.php         wp-includes           wp-login.php          wp-signup.php
bash-5.0$ 

bash-5.0$ wp help
NAME

  wp

DESCRIPTION

  Manage WordPress through the command-line.

SYNOPSIS

  wp <command>

SUBCOMMANDS

  cache                 Adds, removes, fetches, and flushes the WP Object Cache object.
  cap                   Adds, removes, and lists capabilities of a user role.
  cli                   Reviews current WP-CLI info, checks for updates, or views defined aliases.
  comment               Creates, updates, deletes, and moderates comments.
  config                Generates and reads the wp-config.php file.
  core                  Downloads, installs, updates, and manages a WordPress installation.
  cron                  Tests, runs, and deletes WP-Cron events; manages WP-Cron schedules.
  db                    Performs basic database operations using credentials stored in wp-config.php.
  embed                 Inspects oEmbed providers, clears embed cache, and more.
  eval                  Executes arbitrary PHP code.
  eval-file             Loads and executes a PHP file.
  export                Exports WordPress content to a WXR file.
  help                  Gets help on WP-CLI, or on a specific command.
  i18n                  Provides internationalization tools for WordPress projects.
  import                Imports content from a given WXR file.
  language              Installs, activates, and manages language packs.
  maintenance-mode      Activates, deactivates or checks the status of the maintenance mode of a site.
  media                 Imports files as attachments, regenerates thumbnails, or lists registered image sizes.
  menu                  Lists, creates, assigns, and deletes the active theme's navigation menus.
  network               Perform network-wide operations.
  option                Retrieves and sets site options, including plugin and WordPress settings.
  package               Lists, installs, and removes WP-CLI packages.
  plugin                Manages plugins, including installs, activations, and updates.
  post                  Manages posts, content, and meta.
  post-type             Retrieves details on the site's registered post types.
  rewrite               Lists or flushes the site's rewrite rules, updates the permalink structure.
  role                  Manages user roles, including creating new roles and resetting to defaults.
  scaffold              Generates code for post types, taxonomies, plugins, child themes, etc.
  search-replace        Searches/replaces strings in the database.
  server                Launches PHP's built-in web server for a specific WordPress installation.
  shell                 Opens an interactive PHP console for running and testing PHP code.
  sidebar               Lists registered sidebars.
  site                  Creates, deletes, empties, moderates, and lists one or more sites on a multisite installation.
  super-admin           Lists, adds, or removes super admin users on a multisite installation.
  taxonomy              Retrieves information about registered taxonomies.
  term                  Manages taxonomy terms and term meta, with create, delete, and list commands.
  theme                 Manages themes, including installs, activations, and updates.
  transient             Adds, gets, and deletes entries in the WordPress Transient Cache.
  user                  Manages users, along with their roles, capabilities, and meta.
  widget                Manages widgets, including adding and moving them within sidebars.

GLOBAL PARAMETERS

  --path=<path>
      Path to the WordPress files.

  --url=<url>
      Pretend request came from given URL. In multisite, this argument is how the target site is specified.

  --ssh=[<scheme>:][<user>@]<host|container>[:<port>][<path>]
      Perform operation against a remote server over SSH (or a container using scheme of "docker", "docker-compose", "vagrant").

  --http=<http>
      Perform operation against a remote WordPress installation over HTTP.

  --user=<id|login|email>
      Set the WordPress user.

  --skip-plugins[=<plugins>]
      Skip loading all plugins, or a comma-separated list of plugins. Note: mu-plugins are still loaded.

  --skip-themes[=<themes>]
      Skip loading all themes, or a comma-separated list of themes.

  --skip-packages
      Skip loading all installed packages.

  --require=<path>
      Load PHP file before running the command (may be used more than once).

  --[no-]color
      Whether to colorize the output.

  --debug[=<group>]
      Show all PHP errors and add verbosity to WP-CLI output. Built-in groups include: bootstrap, commandfactory, and help.

  --prompt[=<assoc>]
      Prompt the user to enter values for all command arguments, or a subset specified as comma-separated values.

  --quiet
      Suppress informational messages.

  Run 'wp help <command>' to get more information on a specific command.

bash-5.0$ 

bash-5.0$ wp help theme
bash-5.0$ wp theme list
+-----------------+----------+--------+---------+
| name            | status   | update | version |
+-----------------+----------+--------+---------+
| twentynineteen  | inactive | none   | 1.5     |
| twentyseventeen | inactive | none   | 2.3     |
| twentytwenty    | active   | none   | 1.2     |
+-----------------+----------+--------+---------+
bash-5.0$ 

bash-5.0$ wp user list
+----+--------------+--------------+-----------------+---------------------+---------------+
| ID | user_login   | display_name | user_email      | user_registered     | roles         |
+----+--------------+--------------+-----------------+---------------------+---------------+
| 1  | testwp-admin | testwp-admin | lifcn@yahoo.com | 2020-05-10 07:03:58 | administrator |
+----+--------------+--------------+-----------------+---------------------+---------------+
bash-5.0$ 

bash-5.0$ wp post list
+----+--------------+-------------+---------------------+-------------+
| ID | post_title   | post_name   | post_date           | post_status |
+----+--------------+-------------+---------------------+-------------+
| 1  | Hello world! | hello-world | 2020-05-10 07:03:59 | publish     |
+----+--------------+-------------+---------------------+-------------+
bash-5.0$ 

bash-5.0$ wp cron schedule list
+------------+-------------+----------+
| name       | display     | interval |
+------------+-------------+----------+
| hourly     | Once Hourly | 3600     |
| twicedaily | Twice Daily | 43200    |
| daily      | Once Daily  | 86400    |
| weekly     | Once Weekly | 604800   |
+------------+-------------+----------+
bash-5.0$ 

```