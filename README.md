# Magento 2 installation with DDEV

[![Version](https://img.shields.io/github/v/release/julienloizelet/github-actions-magento2-ddev-installation)](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/releases)
[![Installation with Varnish](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/actions/workflows/module-with-varnish-test.yml/badge.svg?event=push)](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/actions/workflows/module-with-varnish-test.yml)
[![Installation with Static and Unit tests](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/actions/workflows/module-with-static-and-unit-tests.yml/badge.svg?event=push)](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/actions/workflows/module-with-static-and-unit-tests.yml)

A GitHub Action for installing Magento 2 with DDEV.


<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [Quick start](#quick-start)
- [Settings](#settings)
- [Usage](#usage)
  - [Use DDEV to interact with your Magento 2 instance](#use-ddev-to-interact-with-your-magento-2-instance)
  - [Test a module](#test-a-module)
    - [Examples](#examples)
    - [How to](#how-to)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Quick start

_We will suppose here that you want to test on a Magento 2.4.5 instance with PHP 8.1._

You can add the following step in your workflow:

```yaml
- uses: julienloizelet/github-actions-magento2-ddev-installation@main
  with:
    php_version: "8.1"
    magento_version: "2.4.5"
```

This step will install a Magento `2.4.5` instance with PHP `8.1`.

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


The Magento 2 environment is a Docker environment created  with [DDEV](https://github.com/drud/ddev) and comes with the 
following 
services:
- `web`: PHP `8.1`, nginx-fpm, NodeJs
- `db`: MariaDb
- `elastisearch`
- `memcached`
- `redis`
- `mailhog`

Inside your workflow, you could access to the website at the url `https://m245.ddev.site`.




Furthermore, as we are using here the default values: 
- Sources come from the [Mage-OS](https://mage-os.org/) composer repository.
- Magento edition is Magento Open Source (CE) (`magento/project-community-edition`).
- Varnish is not used
- There is no `COMPOSER_AUTH` required.

Finally, the structure of your `$GITHUB_WORKSPACE` will look like below.


```markdown
$GITHUB_WORKSPACE
│   
│ (Magento 2 sources installed with composer)    
│
└───.ddev
    │   
    │ (Cloned sources of `julienloizelet/ddev-m2` repo : a Magento 2 DDEV specific repo)
```

## Settings

The following are optional as `step.with` keys:


|         Name         	|   Type  	|               Description              	|               Default               	|                                                                                                        Comments                                                                                                                                                                                                                 	                                                                                                         |
|:--------------------:	|:-------:	|:--------------------------------------:	|:-----------------------------------:	|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|     `php_version`    	| String  	|           PHP Version to use           	|                "8.1"                	|                                                                                                                                                                                                                     	                                                                                                                                                                                                                     |
| `magento_repository` 	| String  	|      Where to install Magento from     	|    "https://mirror.mage-os.org/"    	|                                                                                              For Adobe repository: "https://repo.magento.com/"                                                                                                                                                                                            	                                                                                               |
|   `magento_edition`  	|  String 	|    The edition of Magento to install   	| "magento/project-community-edition" 	|                                                                                            For Adobe Commerce: "magento/project-enterprise-edition"                                                                                                                                                                                         	                                                                                             |
|   `magento_version`  	|  String 	| The Magento release version to install 	|               "2.4.5"               	|                                                      Available versions depend on the chosen `magento_repository`.<br>You can use `X.Y.Z` format or `X.Y.Z-pN` for patch release.<br>The DDEV repo handle only versions from `2.3.0` to `2.4.5` (latest release for now)                                                                                                           	                                                      |
|    `composer_auth`   	|  String 	|   Composer authentication credentials  	|                  ""                 	|                       You have to pass a JSON string. For example:<br>```{    "http-basic": {       "repo.magento.com": {           "username": "**********************",            "password": "*****************"        }    }}```<br><br>As GitHub allows saving multiline secret, you can use a secret to store this sensitive value. For example:<br>```composer_auth: ${{ secrets.M2_COMPOSER_AUTH }}``` 	                        |
|    `varnish_setup`   	| Boolean 	|    Install with ready-to-use Varnish   	|                false                	|You should use quote to set true:  `varnish_setup: "true"`<br><br>For more information, please see [related documentation](https://github.com/julienloizelet/ddev-m2#varnish)                                                                                                                                                                                                                                                            	 |



## Usage

### Use DDEV to interact with your Magento 2 instance

You could run all the DDEV basic commands and some specific ones coming from [my M2/DDEV repo](https://github.com/julienloizelet/ddev-m2).

For example, you could run these commands in some other steps: 

```shell
ddev magento config:set admin/security/password_is_forced 0
ddev magento config:set admin/security/password_lifetime 0
ddev magento module:disable Magento_TwoFactorAuth
ddev magento indexer:reindex
ddev magento c:c
```


### Test a module

Once you have run this action, you will be able to install and activate a module. Thus, you will be able to run all 
kind of tests : static tests (coding standards), unit tests, integration tests, or any other end-to-end tests.

#### Examples

Before reading below, you could read the examples here: 
- [Static and Unit test of a module](.github/workflows/module-with-static-and-unit-tests.yml)
- [Installation and Varnish test of a module](.github/workflows/module-with-varnish-test.yml)


#### How to

To do that, you could use the following folder structure : 

```markdown
$GITHUB_WORKSPACE
│   
│ (Magento 2 sources installed with composer)    
│
└───.ddev
│   │   
│   │ 
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


## License

[MIT](LICENSE)
