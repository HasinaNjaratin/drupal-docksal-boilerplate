This project template provides a starter kit to manage drupal project with [Docksal](https://docksal.io/), [xdebug](https://xdebug.org/) and [grumphp](https://github.com/phpro/grumphp).
It is set with most popular and used modules for drupal, such as [devel](https://www.drupal.org/project/devel), [config_split](https://www.drupal.org/project/config_split), [paragraphs](https://www.drupal.org/project/paragraphs), etc ...

**Table of Contents**

- [Docksal](#docksal)
- [Drupal generator](#drupal-generator)
- [Composer](#composer)
- [Xdebug](#xdebug)
- [Configuration Split](#configuration-split)
- [Translations](#translations)
- [Particular commands](#particular-commands)
- [PHPCS](#phpcs)
- [Grumphp](#grumphp)

# Docksal

First you need to [install docksal](https://docksal.io/installation).

> Note: You might need to install `docker` if you do not yet install it for your setup.

After that you clone this project and run

```
fin init
```

***Monitor the console outputs carefully. The superadmin access will be returned there.***

> Note: Drupal will avalaible through [`http://drupal-boilerplate.docksal:8080/`](http://drupal-boilerplate.docksal:8080/).

# Drupal generator

To create a drupal instance

```
fin init-site
```

will install the drupal website automatically according to configurations you have set in _.docksal/settings/site_config.sh_

> Note: You no longer have to run this command if you have already run the `fin init` command. This is just to let you know that it exists and that you can use it if you want to re-install a new drupal install from the same docksal instance.

# Composer

To install php components, run

```
fin composer install
```

With `composer require ...` you can download new dependencies to your
installation.
Example:
```
fin composer require drupal/devel:~1.0
```

To check component version, run

```
fin composer outdated
```

To update composer packages, run

```
fin composer update
```

#### How can I apply patches to downloaded modules?

If you need to apply patches (depending on the project being modified, a pull
request is often a better solution), you can do so with the
[composer-patches](https://github.com/cweagans/composer-patches) plugin.

To add a patch to drupal module foobar insert the patches section in the extra
section of composer.json:
```
"extra": {
    "patches": {
        "drupal/foobar": {
            "Patch description": "URL or local path to patch"
        }
    }
}
```

Use _/patches_ directory to put patches files.

# Xdebug

This project has a php with an xdebug installed and activated, ready to use.

To set it up with the IDE : [Docksal + xdebug + phpstorm](https://docs.docksal.io/tools/xdebug/)


# Configuration split

Use [config_split](https://www.drupal.org/project/config_split) module to manage configurations.

There are three splits of configurations :
- dev : related to developpement environnement (_/config/splits/dev_)
- hors_prod : related to hors_prod environnement (_/config/splits/hors_prod_)
- prod : related to prod environnement (_/config/splits/prod_)

```
$config['config_split.config_split.dev']['status'] = TRUE;
$config['config_split.config_split.hors_prod']['status'] = FALSE;
$config['config_split.config_split.prod']['status'] = FALSE;
```

To import

```
fin drush cim -y
```

To export

```
fin drush csex -y
```


# Translations

You need to manage po files to configure multilanguage site case.

Translations directory is stored (configured) _/config/translations_

To check for updates

```
fin drush locale-check
```

To update

```
fin drush locale-update
```

# Particular commands

To reinstall composer package, remove vendor, core and contrib modules/themes :

```
fin reinstall
```

To install or update local environment : install new components, update database, import configurations, etc ...

```
fin update-site
```

# Phpcs

Phpcs is necessary to control and continue coding in good practice.

The verification is done in the _/www/modules/custom_ directory.

- Run phpcs to list all php code style evaluations :

```
fin phpcs
```

- Run phpcsf to fix all php code style evaluations that can be fixed automatically :

```
fin phpcs-fix
```

- Run phpcs to summary php code style evaluations :

```
fin phpcs-summary
```

# Grumphp

[grumphp](https://github.com/phpro/grumphp) is used to check the quality of codes before commits.

[PhpLint](https://github.com/phpro/grumphp/blob/master/doc/tasks/phplint.md), [PhpUnit](https://github.com/phpro/grumphp/blob/master/doc/tasks/phplint.md) and [PhpCs](https://github.com/phpro/grumphp/blob/master/doc/tasks/phpcs.md) are launched at each commit.

> Note: phpro/grumphp is fixed in 0.18.1 version because at the moment I write this doc, the recent version of grumphp is not compatible (has conflit) with some drupal dependencies.

[Look]()
