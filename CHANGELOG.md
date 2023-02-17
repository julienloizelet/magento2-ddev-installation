# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en)
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).


## [1.6.0](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/releases/tag/v1.6.0) - 2023-02-17
[_Compare with previous release_](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/compare/v1.5.0...v1.6.0)

### Changed

- Exclude `magento/composer` from packagist repository ([magento/composer/issues/#34](https://github.com/magento/composer/issues/34#issuecomment-1432920391))
- Do not exclude `magento/composer-dependency-version-audit-plugin` from composer magento repository

---

## [1.5.0](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/releases/tag/v1.5.0) - 2023-02-16
[_Compare with previous release_](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/compare/v1.4.0...v1.5.0)

### Changed

- Exclude `magento/composer-dependency-version-audit-plugin` from composer magento repository
- Changed default `ddev_repository_ref` input value to `v2.7.1`

---


## [1.4.0](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/releases/tag/v1.4.0) - 2023-02-13
[_Compare with previous release_](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/compare/v1.3.0...v1.4.0)

### Changed

- Replace deprecated set-output command
- Changed default `ddev_repository_ref` input value to `v2.7.0`


---

## [1.3.0](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/releases/tag/v1.3.0) - 2022-09-16
[_Compare with previous release_](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/compare/v1.2.0...v1.3.0)

### Changed

- Changed default `ddev_repository_ref` input value to `v2.5.0` for Magento Functional Testing Framework (MFTF) 
---

## [1.2.0](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/releases/tag/v1.2.0) - 2022-08-26
[_Compare with previous release_](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/compare/v1.1.0...v1.2.0)

### Added

- Add `m2_url` output to retrieve freshly installed Magento 2 instance url
---
## [1.1.0](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/releases/tag/v1.1.0) - 2022-08-26
[_Compare with previous release_](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/compare/v1.0.0...v1.1.0)
### Added

- Add `ddev_repository_ref` input to allow choosing version, branch or commit sha of `ddev-m2` repo

### Changed

- Use expected DDEV version as set in the `ddev-m2` repo
---
## [1.0.0](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/releases/tag/v1.0.0) - 2022-08-22
[_Compare with previous release_](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/compare/v0.0.1...v1.0.0)
### Added
- Stable release
---
## [0.0.1](https://github.com/julienloizelet/github-actions-magento2-ddev-installation/releases/tag/v0.0.1) - 2022-08-19

### Added
- Initial release
