## Qooxdoo Package Cache

![Update Package Cache](https://github.com/qooxdoo/package-cache/workflows/Update%20Package%20Cache/badge.svg)

This repository is part of the qooxdoo package system, qooxdoo's "plugin" architecture. Packages contain qooxdoo libraries that can be loaded on-demand, using a command line interface.

We store a cache of json data here which is generated nightly from querying the GitHub API and can be donwloaded by executing npx qx package update. If you need more frequent updates, use `npx qx package update --search`. Note that you have to set a GitHub Token first, using `npx qx config set github.token <your token>`.

For reasons of security and quality assurance, whenever a package release is detected in the nightly cron job, a PR is created that needs to be reviewed by the qooxdoo team. One review is sufficient to merge the PR.

<script defer="defer" type="application/javascript">
(async () => {
    let cache = await (await fetch("https://raw.githubusercontent.com/qooxdoo/package-cache/master/cache.json")).json();
    document.writeln(`<div>Number of releases: ${cache.num_libraries}</div>`);
    document.writeln(`<h3>Latest releases</h3>`);
    let table_html = `<table><th><td>Repository Name</td><td>Version</td><td>Description</td></th>`;
    for (let repo of cache.repos.list) {
        let data = cache.repos.data[repo];
        let releases = data.releases.list;
        let latest_release = releases[releases.length-1] || "";
        table_html += `<tr><td>${repo}</td><td>${latest_release}</td><td>${data.description}</td></tr>`;
    }
    document.writeln(table_html + `</table>`);
})();
</script>

 
