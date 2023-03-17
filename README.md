# Magento 2 installation with DDEV

[![Version](https://img.shields.io/github/v/release/julienloizelet/magento2-ddev-installation)](https://github.com/julienloizelet/magento2-ddev-installation/releases)
![project is maintained](https://img.shields.io/maintenance/yes/2023.svg)
[![Installation with Varnish](https://github.com/julienloizelet/magento2-ddev-installation/actions/workflows/module-with-varnish-test.yml/badge.svg)](https://github.com/julienloizelet/magento2-ddev-installation/actions/workflows/module-with-varnish-test.yml)
[![Installation with Static and Unit tests](https://github.com/julienloizelet/magento2-ddev-installation/actions/workflows/module-with-static-and-unit-tests.yml/badge.svg)](https://github.com/julienloizelet/magento2-ddev-installation/actions/workflows/module-with-static-and-unit-tests.yml)
[![End-to-end tests](https://github.com/julienloizelet/magento2-ddev-installation/actions/workflows/module-with-end-to-end-tests.yml/badge.svg)](https://github.com/julienloizelet/magento2-ddev-installation/actions/workflows/module-with-end-to-end-tests.yml)
[![MFTF tests](https://github.com/julienloizelet/magento2-ddev-installation/actions/workflows/mftf-tests.yml/badge.svg)](https://github.com/julienloizelet/magento2-ddev-installation/actions/workflows/mftf-tests.yml)

A GitHub Action to install Magento 2 with [DDEV](https://github.com/ddev/ddev).


<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [Quick start](#quick-start)
- [Inputs](#inputs)
  - [Available keys](#available-keys)
  - [Examples](#examples)
- [Outputs](#outputs)
- [Usage](#usage)
  - [Test your Magento 2 instance](#test-your-magento-2-instance)
  - [Test a module](#test-a-module)
- [Technical details](#technical-details)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Quick start

_We will suppose here that you want to test on a Magento 2.4.5 instance with PHP 8.1._

You can add the following step in your workflow:

```yaml
- uses: julienloizelet/magento2-ddev-installation@v2.0.0
  with:
    php_version: "8.1"
    magento_version: "2.4.5"
```

This step will install a Magento `2.4.5` instance with PHP `8.1`.

In the steps that follow, you will be able to run any DDEV commands to interact with the Magento 2 environment.


## Inputs


### Available keys

The following keys are available as `step.with` keys:

---
- `php_version` (_String_)

PHP version to use in the web container.

Default: `8.2`.

Allowed values are: `7.2`, `7.3`, `7.4`, `8.1`, `8.2`.

Please choose a PHP version that is compatible with the `magento_version` below.

---
- `magento_repository` (_String_)

Where to install Magento from. 

Default: `https://mirror.mage-os.org/`.

Could be "https://mirror.mage-os.org/", "https://repo.magento.com/" or any available repository.

Please choose a repository that handle the `magento_version` below.

---
- `magento_edition` (_String_)

The edition of Magento to install. 

Default: `magento/project-community-edition`

Could be "magento/project-community-edition", "magento/project-enterprise-edition" or any available edition.

---
- `magento_version` (_String_)

The Magento release version to install.  

Default: `2.4.6`.

You can use `X.Y.Z` format or `X.Y.Z-pN` format for patch release.

Allowed versions are `2.3.0`, `2.3.1`, `2.3.2`, `2.3.3`, `2.3.4`, `2.3.5`, `2.3.6`, `2.3.7`, `2.4.0`,
  `2.4.1`, `2.4.2`, `2.4.3`,`2.4.4`, `2.4.5`, `2.4.6` and any of their patches versions. 

Please note that available versions depend on the chosen `magento_repository`.

---
- `composer_auth` (_String_)

Composer authentication credentials. 

Default: `""`.


You have to pass a JSON string. For example:
```json
{
  "http-basic": {
    "repo.magento.com": {
      "username": "**********************",
      "password": "**********************"
    }
  }
}
```
As GitHub allows saving multiline secret, you can use a secret to store this sensitive value. Just copy/paste the 
json in a `M2_COMPOSER_AUTH` secret and use it like this: `composer_auth: ${{ secrets.M2_COMPOSER_AUTH }}`.

---

- `varnish_setup` (_Boolean_)

Install with ready-to-use Varnish. 

Default: `false`.


You should use quote to set true:  `varnish_setup: "true"`.

---


### Examples

- Magento `2.3.7-p4` (`magento/project-community-edition`) , from `https://repo.magento.com/`, with PHP `7.4` and 
  without Varnish:

```
with:
  php_version: "7.4"
  magento_version: "2.3.7-p4"
  magento_repository: "https://repo.magento.com/"
  composer_auth: ${{ secrets.M2_COMPOSER_AUTH }}
```

- Magento `2.4.4` (`magento/project-community-edition`) , from `https://mirror.mage-os.org/`, with PHP `8.1` and
  with Varnish:


```
with:
  php_version: "8.1"
  magento_version: "2.4.4"
  varnish_setup: "true"
```

## Outputs

The following keys are available as `outputs` keys:

---
- `m2_url` (_String_)

The freshly installed Magento 2 instance url. Example: `https://m245.ddev.site`.


---



## Usage

### Test your Magento 2 instance

You could run all the DDEV basic commands and some specific ones coming from some DDEV add-ons


#### Examples

For example, you could run these commands in some other steps: 

```shell
ddev magento config:set admin/security/password_is_forced 0
ddev magento config:set admin/security/password_lifetime 0
ddev magento module:disable Magento_TwoFactorAuth
ddev magento indexer:reindex
ddev magento c:c
```

#### MFTF

If you want to use the [Magento Functional Testing Framework](https://devdocs.magento.com/mftf/docs/introduction.html),
here is an example of implementation : [MFTF tests](.github/workflows/mftf-tests.yml)


### Test a module

Once you have run this action, you will be able to install and activate a module. Thus, you will be able to run all 
kind of tests : static tests (coding standards), unit tests, integration tests, or any other end-to-end tests.

#### Examples

Before reading below, you could read the examples here: 
- [Static and Unit test of a module](.github/workflows/module-with-static-and-unit-tests.yml)
- [Installation and Varnish test of a module](.github/workflows/module-with-varnish-test.yml)
- [End-to-end tests of a module](.github/workflows/module-with-end-to-end-tests.yml)


#### How to

To do that, you could use the following folder structure : 

```markdown
$GITHUB_WORKSPACE
│   
│ (Magento 2 sources installed with composer)    
│
└───.ddev
│   │   
│   │ (DDEV files)
│   
└───my-own-modules
    │   
    │
    └───<some-path>
       │   
       │ (Sources of a module)
         
```


by adapting the following steps: 

```yaml
- name: Clone module files
  uses: actions/checkout@v3
  with:
    path: my-own-modules/<some-path>
```

```yaml
- name: Prepare composer repositories
  run: |
      ddev composer config --unset repositories.0
      ddev composer config repositories.0 '{"type": "path", "url":"my-own-modules/<some-path>",  "canonical": true, "options": {"symlink": false}}'
      ddev composer config repositories.1 '{"type": "composer", "url":"<the-magento-repository>",  "exclude": ["<some-package-name>"]}'
```

```yaml
- name: Add module as composer dependency
  run: ddev composer require <some-package-name>:@dev --no-interaction
```

```yaml
- name: Install module
  run: |
    ddev magento module:enable <some-extension-name>
    ddev magento setup:upgrade
```


Then, you could run: 


- PHP Code Sniffer: `ddev phpcs my-own-modules/<some-path>`
- PHP Mess Detector: `ddev phpmd my-own-modules/<some-path>`
- PHP Stan: `ddev phpstan my-own-modules/<some-path>`
- Unit test: `ddev phpunit my-own-modules/<some-path>/Test/Unit`



## Technical details

For you information, the setup of Magento 2 is launch with the following settings:

```shell
bin/magento setup:install \
   --base-url=https://m245.ddev.site \
   --db-host=db \
   --db-name=db \
   --db-user=db \
   --db-password=db \
   --backend-frontname=admin \
   --admin-firstname=admin \
   --admin-lastname=admin \
   --admin-email=admin@admin.com \
   --admin-user=admin \
   --admin-password=admin123 \
   --language=en_US \
   --currency=USD \
   --timezone=America/Chicago \
   --use-rewrites=1 \
   --elasticsearch-host=elasticsearch
```


The Magento 2 environment is a Docker environment created  with DDEV and comes with the following services:
- `web`: PHP `8.1`, nginx-fpm, NodeJs
- `db`: MariaDb
- `elastisearch`
- `memcached`
- `redis`
- `mailhog`


Finally, the structure of your `$GITHUB_WORKSPACE` will look like below.


```markdown
$GITHUB_WORKSPACE
│   
│ (Magento 2 sources installed with composer)    
│
└───.ddev
    │   
    │ (DDEV files)
```

## License

[MIT](LICENSE)
