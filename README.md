#  Qooxdoo Package Cache 

![Update Package Cache](https://github.com/qooxdoo/package-cache/workflows/Update%20Package%20Cache/badge.svg)

This repository is part of the qooxdoo package system, qooxdoo's "plugin"
architecture. Packages contain qooxdoo libraries that can be loaded on-demand,
using a
[command line interface](http://www.qooxdoo.org/docs/#/cli/packages).

We store a cache of json data here which is generated **daily** from querying
the GitHub API. If you need more frequent updates, use a GitHub Access token
with your CLI commands. Please **do not rely** on the structure of this data, as
it can change any time.
