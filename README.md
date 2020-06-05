#  Qooxdoo Package Cache 

![Update Package Cache](https://github.com/qooxdoo/package-cache/workflows/Update%20Package%20Cache/badge.svg)

This repository is part of the qooxdoo package system, qooxdoo's "plugin"
architecture. Packages contain qooxdoo libraries that can be loaded on-demand,
using a [command line interface](http://www.qooxdoo.org/docs/#/cli/packages).

We store a cache of json data here which is generated nightly from querying
the GitHub API and can be donwloaded by executing `npx qx package update`. 
If you need more frequent updates, use a  `npx qx package update --search`. 
Note that you have to set a GitHub Token first, using `npx qx config set github.token <your token>`.

For reasons of security and quality assurance, whenever a package release is detected 
in the nightly cron job, a PR is created that needs to be reviewed by the qooxdoo 
team. One review is sufficient to merge the PR. 

Please **do not rely** on the structure of this data, as it can change any time.
If you need package metadata, use `qx package list --json`.
