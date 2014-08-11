# Drupal Drop Ship

Uses kw_manifests to provide a reusable deployment composed of manifests.

## Usage

Install like any other drupal module and run `drush kw-m`

## What it does

Under the sheets, this algorithm will be executed

1. run database updates
2. ensure ONLY the proper modules are enabled
  * This is a manifest made with code cribbed from the kw-amd command
  * It reads a list of 'seed' modules with which to build the dependency graph
    from the DROPSHIP_SEEDS environment variable
3. revert all features

## Roadmap

We will likely drop kw_manifests soon, since we would like to be able to provide
manifests that operate on the site without fully bootstrap'ing, eg for install
or for applying fixes to known broken states.

This project is opinionated in that it assumes you have already configured all
your backing services (like your database) and you just need to tell Drupal how
to connect to them, and that manifests are for operating on one site. As such,
we can use a composer paradigm and just load the autoloader in settings.php and
use whatever php tools we want, like codegyre/robo or chh/bob and we could
refrain from maintaining our own logic for manifest dependencies. This seems
better than cargo culting the kw_manifests logic if we are going to have to
implement a bootstrap-aware layer anyway.
