# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en)
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## Public API

The [public API](https://semver.org/spec/v2.0.0.html#spec-item-1) of this project is defined by the `action.yaml` file.

---

## [4.0.0](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v4.0.0) - 2025-04-10
[_Compare with previous release_](https://github.com/julienloizelet/magento2-ddev-installation/compare/v3.1.1...v4.0.0)

### Changed

- **Breaking change**: Use `2.4.8` as default Magento version
- **Breaking change**: Use `8.3` as default PHP version

### Added

- Add compatibility with Magento `2.4.8`
- Use `opensearch` search engine for Magento >= `2.4.8`


## [3.1.1](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v3.1.1) - 2024-10-18
[_Compare with previous release_](https://github.com/julienloizelet/magento2-ddev-installation/compare/v3.1.0...v3.1.1)

### Fixed

- Fix a bug introduced with ddev 1.23.5 during composer config command

---

## [3.1.0](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v3.1.0) - 2024-04-20
[_Compare with previous release_](https://github.com/julienloizelet/magento2-ddev-installation/compare/v3.0.0...v3.1.0)

### Changed

- Use `mariadb:10.4` as default database for Magento >= `2.4.1`
- Use `mariadb:10.2` as default database for Magento < `2.4.1`


### Add

- Add `database` input to allow choosing database version and type


### Fixed

- Remediate command injection vulnerabilities by using intermediate environment variables

---


## [3.0.0](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v3.0.0) - 2024-04-11
[_Compare with previous release_](https://github.com/julienloizelet/magento2-ddev-installation/compare/v2.1.1...v3.0.0)

### Changed

- **Breaking change**: Use `2.4.7` as default Magento version
- **Breaking change**: Use `8.2` as default PHP version

### Added

- Add compatibility with Magento `2.4.7`


---

## [2.1.1](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v2.1.1) - 2023-07-25
[_Compare with previous release_](https://github.com/julienloizelet/magento2-ddev-installation/compare/v2.1.0...v2.1.1)

### Fixed

- Fix `omit-containers` option for DDEV 1.22.0+ (`dba` is not allowed anymore)


---


## [2.1.0](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v2.1.0) - 2023-03-17
[_Compare with previous release_](https://github.com/julienloizelet/magento2-ddev-installation/compare/v2.0.0...v2.1.0)

### Changed

- Remove useless files copy as `ddev-tools` add-on already copied files


---

## [2.0.0](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v2.0.0) - 2023-03-15
[_Compare with previous release_](https://github.com/julienloizelet/magento2-ddev-installation/compare/v1.5.0...v2.0.0)

### Changed

- Use DDEV add-ons instead of `julienloizelet/ddev-m2` as DDEV specifics sources 
- Changed default `magento_version` input value to `2.4.6`
- Changed default `php_version` input value to `8.2`

### Added
- Add Magento `2.4.6` compatibility

---

## [1.5.0](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v1.5.0) - 2023-02-16
[_Compare with previous release_](https://github.com/julienloizelet/magento2-ddev-installation/compare/v1.4.0...v1.5.0)

### Changed

- Exclude `magento/composer-dependency-version-audit-plugin` from composer magento repository
- Changed default `ddev_repository_ref` input value to `v2.7.1`

---


## [1.4.0](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v1.4.0) - 2023-02-13
[_Compare with previous release_](https://github.com/julienloizelet/magento2-ddev-installation/compare/v1.3.0...v1.4.0)

### Changed

- Replace deprecated set-output command
- Changed default `ddev_repository_ref` input value to `v2.7.0`


---

## [1.3.0](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v1.3.0) - 2022-09-16
[_Compare with previous release_](https://github.com/julienloizelet/magento2-ddev-installation/compare/v1.2.0...v1.3.0)

### Changed

- Changed default `ddev_repository_ref` input value to `v2.5.0` for Magento Functional Testing Framework (MFTF) 
---

## [1.2.0](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v1.2.0) - 2022-08-26
[_Compare with previous release_](https://github.com/julienloizelet/magento2-ddev-installation/compare/v1.1.0...v1.2.0)

### Added

- Add `m2_url` output to retrieve freshly installed Magento 2 instance url
---
## [1.1.0](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v1.1.0) - 2022-08-26
[_Compare with previous release_](https://github.com/julienloizelet/magento2-ddev-installation/compare/v1.0.0...v1.1.0)
### Added

- Add `ddev_repository_ref` input to allow choosing version, branch or commit sha of `ddev-m2` repo

### Changed

- Use expected DDEV version as set in the `ddev-m2` repo
---
## [1.0.0](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v1.0.0) - 2022-08-22
[_Compare with previous release_](https://github.com/julienloizelet/magento2-ddev-installation/compare/v0.0.1...v1.0.0)
### Added
- Stable release
---
## [0.0.1](https://github.com/julienloizelet/magento2-ddev-installation/releases/tag/v0.0.1) - 2022-08-19

### Added
- Initial release
