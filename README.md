This project template provides a starter kit to manage drupal project with composer and [grumphp](https://github.com/phpro/grumphp).
It is set with most popular and used modules for drupal, such as [devel](https://www.drupal.org/project/devel), [config_split](https://www.drupal.org/project/config_split), [paragraphs](https://www.drupal.org/project/paragraphs), etc ...

**Table of Contents**

- [Composer](#composer)
- [Xdebug](#xdebug)
- [Configuration Split](#configuration-split)
- [Translations](#translations)
- [PHPCS](#phpcs)
- [Grumphp](#grumphp)

# Composer

To install php components, run

```
composer install
```

With `composer require ...` you can download new dependencies to your
installation.
Example:
```
composer require drupal/devel:~1.0
```

To check component version, run

```
composer outdated
```

To update composer packages, run

```
composer update
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

To set it up with the IDE : [xdebug + phpstorm](https://www.jetbrains.com/help/phpstorm/configuring-xdebug.html)


# Configuration split

Use [config_split](https://www.drupal.org/project/config_split) module to manage configurations.

There are three splits of configurations :
- dev : related to developpement environnement (_/config/splits/dev_)
- hors_prod : related to hors_prod environnement (_/config/splits/hors_prod_)
- prod : related to prod environnement (_/config/splits/prod_)

in settings.php

```
$config['config_split.config_split.dev']['status'] = TRUE;
$config['config_split.config_split.hors_prod']['status'] = FALSE;
$config['config_split.config_split.prod']['status'] = FALSE;
```

To import

```
drush cim -y
```

To export

```
drush csex -y
```


# Translations

You need to manage po files to configure multilanguage site case.

Translations directory is stored (configured) _/config/translations_

To check for updates

```
drush locale-check
```

To update

```
drush locale-update
```


# Phpcs

Phpcs is necessary to control and continue coding in good practice.

The verification is done in the _/www/modules/custom_ directory.

- Run phpcs to list all php code style evaluations :

```
./vendor/bin/phpcs --standard=Drupal,DrupalPractice -p --colors ./www/modules/custom
```

- Run phpcsf to fix all php code style evaluations that can be fixed automatically :

```
./vendor/bin/phpcbf --standard=Drupal,DrupalPractice -p --colors ./www/modules/custom
```

- Run phpcs to summary php code style evaluations :

```
./vendor/bin/phpcs --report=summary --standard=Drupal,DrupalPractice -p --colors ./www/modules/custom
```

# Grumphp

[grumphp](https://github.com/phpro/grumphp) is used to check the quality of codes before commits.

[PhpLint](https://github.com/phpro/grumphp/blob/master/doc/tasks/phplint.md), [PhpUnit](https://github.com/phpro/grumphp/blob/master/doc/tasks/phplint.md) and [PhpCs](https://github.com/phpro/grumphp/blob/master/doc/tasks/phpcs.md) are launched at each commit.

> Note: phpro/grumphp is fixed in 0.18.1 version because at the moment I write this doc, the recent version of grumphp is not compatible (has conflit) with some drupal dependencies.
