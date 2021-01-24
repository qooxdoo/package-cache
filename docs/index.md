## Qooxdoo Package Cache

![Update Package Cache](https://github.com/qooxdoo/package-cache/workflows/Update%20Package%20Cache/badge.svg)

This repository is part of the qooxdoo package system,
qooxdoo's "plugin" architecture. Packages contain qooxdoo
libraries that can be loaded on-demand, using [a command line
interface](https://qooxdoo.org/documentation/#/development/cli/packages).

For more information on the individual packages, please view the online 
[Qooxdoo Package Browser ](https://qooxdoo.org/qxl.packagebrowser/) which also
contains live demos of the packages. Please note that the Package Viewer might not
be up-to-date - it is updated nightly. 

# Latest releases

<div id="releases"></div>

<script defer="defer" type="application/javascript">
(async () => {
    let cache = await (await fetch("https://raw.githubusercontent.com/qooxdoo/package-cache/master/cache.json")).json();
    let html = [];
    html.push(`<div>Number of releases: ${cache.num_libraries}</div>`);
    html.push(`<table>`);
    html.push(`<th><td>Repository Name</td><td>Version</td><td>Description</td></th>`);
    for (let repo of cache.repos.list) {
        let data = cache.repos.data[repo];
        let releases = data.releases.list;
        let latest_release = releases[releases.length-1] || "";
        html.push(`<tr><td>${repo}</td><td>${latest_release}</td><td>${data.description}</td></tr>`);
    }
    html.push(`</table>`);
    document.getElementById("releases").innerHTML = html.join("\n");
})();
</script>
