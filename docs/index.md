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

# Package releases

<div>[ <a onclick="create_table();">Alphabetically</a>] [ <a onclick="create_table(1);">Last released</a>]</div>
<div id="releases"></div>
<script defer="defer" type="application/javascript">
async function create_table(by_date=false) {
    let cache = await (await fetch("https://raw.githubusercontent.com/qooxdoo/package-cache/master/cache.json")).json();
    let html = [];
    html.push(`<div>Number of releases: ${cache.num_libraries}</div>`);
    html.push(`<table>`);
    html.push(`<thead><tr><td>Repository Name</td><td>Latest Version</td><td>Description</td></tr></thead>`);
    html.push(`<tbody>`);
    let releases_by_date = {};
    let releases_table = [];
    for (let repo of cache.repos.list) {
        let data = cache.repos.data[repo];
        let releases_list = data.releases.list;
        let latest_release = releases_list[releases_list.length-1] || "";
        if (latest_release && by_date) {
            let published_at = data.releases.data[latest_release].published_at;
            releases_by_date[published_at] = releases_table.length;
            releases_table.push(`<tr><td>${repo}</td><td>${latest_release} (${published_at})</td><td>${data.description}</td></tr>`);
        } else {
            releases_table.push(`<tr><td>${repo}</td><td>${latest_release}</td><td>${data.description}</td></tr>`);
        }
    }
    html.push( by_date 
        ? Object.keys(releases_by_date).sort().reverse().map(date => releases_table[releases_by_date[date]]).join("\n")
        : releases_table.join("\n")
    );
    html.push(`</tbody></table>`);
    document.getElementById("releases").innerHTML = html.join("\n");
}
create_table();
</script>
