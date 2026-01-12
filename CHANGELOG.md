# Changelog

## Unreleased

### Features

* add Suricata dashboard, saved searches, and KV store baseline collections
* refactor dashboards (overview, DNSBL, IP log, host, detail) with updated panels and layout
* add filterlog normalization macros/transforms and document panel sources

### Bug Fixes

* fix `rule_origin_tok` evaluation in `pfsense_filterlog_base` macro
* reduce result counts for external blocked sources and internal talkers to improve performance
* remove deprecated insights dashboard assets

## [1.1.0](https://github.com/ptmetcalf/pfsense-dashboards/compare/v1.0.1...v1.1.0) (2026-01-12)


### Miscellaneous Chores

* release-as 1.1.0 ([5dc2b00](https://github.com/ptmetcalf/pfsense-dashboards/commit/5dc2b0080fa29d13f5c410ee24f87ee3e7d06e32))

## [1.0.1](https://github.com/ptmetcalf/pfsense-dashboards/compare/v1.0.0...v1.0.1) (2026-01-04)


### Bug Fixes

* remove redundant APP_NAME variable assignment in release workflow ([5a702ba](https://github.com/ptmetcalf/pfsense-dashboards/commit/5a702ba7e838a13ff79dcfffc353c58a63ce0951))

## [1.0.0](https://github.com/ptmetcalf/pfsense-dashboards/compare/v1.0.0...v1.0.0) (2026-01-04)


### Features

* add CI workflow for automated app inspection and packaging ([cda6df0](https://github.com/ptmetcalf/pfsense-dashboards/commit/cda6df0c1dc14058935f6e4c10edda918f979b30))
* ensure package does not check for updates ([3ec25fe](https://github.com/ptmetcalf/pfsense-dashboards/commit/3ec25fe8d24c7b6a81632c8fc16c6360cf9f5048))
* initial release ([a02dae6](https://github.com/ptmetcalf/pfsense-dashboards/commit/a02dae63d8d2166652a84359352ff708b11b36ae))
* update release process to use GitHub CLI for asset uploads ([53d3339](https://github.com/ptmetcalf/pfsense-dashboards/commit/53d3339a5f6e592056b7e0deb871c5deb112bc43))
* update release workflow to trigger on workflow_run and remove tag push event ([20618dc](https://github.com/ptmetcalf/pfsense-dashboards/commit/20618dc4984c9d3dbdc9205404b3792309d98776))
* update release workflow, enhance AppInspect instructions, and modify manifest for versioning ([09941b9](https://github.com/ptmetcalf/pfsense-dashboards/commit/09941b9d11b2cd8fd760ca43f17130d81053d398))


### Bug Fixes

* correct dependency casing and update platform requirements ([795a390](https://github.com/ptmetcalf/pfsense-dashboards/commit/795a39081eda71eed7b6da0f0a88c0c64c07bc50))
* revert schema version and update platform requirements for compatibility ([9dd5c35](https://github.com/ptmetcalf/pfsense-dashboards/commit/9dd5c35b8e2728993eef30d8fe6baf97512575e9))
