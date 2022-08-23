# BiocCheck Action

[![BiocCheck action test](https://github.com/insightsengineering/bioc-check-action/actions/workflows/test-action.yaml/badge.svg)](https://github.com/insightsengineering/bioc-check-action/actions/workflows/test-action.yaml)
[![BiocCheck action test no cache](https://github.com/insightsengineering/bioc-check-action/actions/workflows/test-action-no-cache.yaml/badge.svg)](https://github.com/insightsengineering/bioc-check-action/actions/workflows/test-action-no-cache.yaml)
[![SuperLinter](https://github.com/insightsengineering/bioc-check-action/actions/workflows/linter.yaml/badge.svg)](https://github.com/insightsengineering/bioc-check-action/actions/workflows/linter.yaml)

## Description

Github Action that implements Bioconductor-specific R package checks with [BiocCheck](https://bioconductor.org/packages/release/bioc/html/BiocCheck.html).

## Action Type

Composite

## Quick Start

1. Create a new GitHub Actions workflow file `.github/workflows/bioc-check.yaml` and add the following as content:

```yaml
---
name: BiocCheck

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  bioc-check:
    runs-on: ubuntu-latest
    name: BiocCheck
    container:
      image: rocker/verse:4.2.1
    steps:
      - name: Checkout repo
        uses: actions/checkout@v4

      - name: Run R CMD check
        run: |
          R CMD build .
          R CMD INSTALL *.tar.gz
          R CMD check *.tar.gz

      - name: Run BiocCheck
        uses: insightsengineering/bioc-check-action@v1

```

2. Create a PR against your repository to test and use the action.

## Standalone Usage

Note that you may also use the script from this action in standalone mode by running the following:

```bash
# Download the script
wget -O BiocCheck.R \
  https://raw.githubusercontent.com/insightsengineering/bioc-check-action/main/BiocCheck.R
# Making the script executable
chmod +x BiocCheck.R
# Run the script
./BiocCheck.R --help
```

## Example Output

You may view an example output of this action [here](https://github.com/insightsengineering/hermes/pull/166#issuecomment-1016147947).

## Inputs

* `path`:

  _Description_: Path to package's root

  _Required_: `false`

  _Default_: `.`

* `new-package`:

  _Description_: enable checks specific to new packages

  _Required_: `false`

  _Default_: `false`

* `post-result-as-comment`:

  _Description_: post the check result as a PR comment

  _Required_: `false`

  _Default_: `true`

* `no-check-dependencies`:

  _Description_: disable check for bad dependencies

  _Required_: `false`

  _Default_: `false`

* `no-check-deprecated`:

  _Description_: disable check for usage of deprecated packages

  _Required_: `false`

  _Default_: `false`

* `no-check-remotes`:

  _Description_: disable check for usage of remote packages other than those hosted on CRAN or Bioconductor

  _Required_: `false`

  _Default_: `false`

* `no-check-version-num`:

  _Description_: disable check for valid version number

  _Required_: `false`

  _Default_: `false`

* `no-check-R-ver`:

  _Description_: disable check for valid R version

  _Required_: `false`

  _Default_: `false`

* `no-check-pkg-size`:

  _Description_: disable check for package tarball size

  _Required_: `false`

  _Default_: `false`

* `no-check-file-size`:

  _Description_: disable check for individual file size

  _Required_: `false`

  _Default_: `false`

* `no-check-bioc-views`:

  _Description_: disable biocViews-specific checks (for non-BioC packages)

  _Required_: `false`

  _Default_: `false`

* `no-check-bbs`:

  _Description_: disable BBS-specific checks (for non-BioC packages). Valid DESCRIPTION

  _Required_: `false`

  _Default_: `false`

* `no-check-description`:

  _Description_: disable DESCRIPTION file checks

  _Required_: `false`

  _Default_: `false`

* `no-check-namespace`:

  _Description_: disable namespace checks

  _Required_: `false`

  _Default_: `false`

* `no-check-vignettes`:

  _Description_: disable vignette checks

  _Required_: `false`

  _Default_: `false`

* `no-check-library-calls`:

  _Description_: disable check usage of functions that install or update packages

  _Required_: `false`

  _Default_: `false`

* `no-check-install-self`:

  _Description_: disable check for require or library of itself

  _Required_: `false`

  _Default_: `false`

* `no-check-coding-practices`:

  _Description_: disable check for some common best coding practices

  _Required_: `false`

  _Default_: `false`

* `no-check-function-len`:

  _Description_: disable check for function length

  _Required_: `false`

  _Default_: `false`

* `no-check-man-doc`:

  _Description_: disable checks for man page documentation

  _Required_: `false`

  _Default_: `false`

* `no-check-news`:

  _Description_: disable checks for NEWS file

  _Required_: `false`

  _Default_: `false`

* `no-check-unit-tests`:

  _Description_: disable checks for unit tests

  _Required_: `false`

  _Default_: `false`

* `no-check-skip-bioc-tests`:

  _Description_: disable check for tests that skip when on bioc

  _Required_: `false`

  _Default_: `false`

* `no-check-formatting`:

  _Description_: disable checks for file formatting

  _Required_: `false`

  _Default_: `false`

* `no-check-CRAN`:

  _Description_: disable check for if package exists in CRAN

  _Required_: `false`

  _Default_: `false`

* `no-check-bioc-help`:

  _Description_: disable check for registration on Bioconductor mailing list and support site

  _Required_: `false`

  _Default_: `false`

* `build-output-file`:

  _Description_: file containing R CMD build output, for additional analysis

  _Required_: `false`

* `quit-with-status`:

  _Description_: enable exit code option when performing check

  _Required_: `false`

  _Default_: `false`

* `no-cache`:

  _Description_: disable github action R dependency caching

  _Required_: `false`

  _Default_: `false`

* `cache-version`:

  _Description_: version of cache. To clean cache bump this version

  _Required_: `false`

  _Default_: `cache-v1`

* `allow-failure`:

  _Description_: BiocCheck errors will not fail, but will give a warning

  _Required_: `false`

  _Default_: `false`
