![Update Package Cache](https://github.com/qooxdoo/package-cache/workflows/Update%20Package%20Cache/badge.svg)

The qooxdoo package system is qooxdoo's "plugin" architecture. Packages
contain qooxdoo libraries that can be loaded on-demand, using [a command line
interface](https://qooxdoo.org/documentation/#/development/cli/packages).

For more information on the individual packages, please view the online 
[Qooxdoo Package Browser ](https://qooxdoo.org/qxl.packagebrowser/) which also
contains live demos of the packages. Please note that the Package Viewer might not
be up-to-date - it is updated nightly. 

### Package releases

<div>[ <a onclick="create_table();">Alphabetically</a>] [ <a onclick="create_table(1);">Last released</a>]</div>

<div id="releases"></div>
<script defer="defer" type="application/javascript">
async function create_table(by_date=false) {
    let cache = await (await fetch("https://raw.githubusercontent.com/qooxdoo/package-cache/master/cache.json")).json();
    let html = [];
    html.push(`<div>Number of releases: ${cache.num_libraries}</div>`);
    html.push(`<table>`);
    html.push(`<thead><tr><td>Repository Name</td><td>Latest Version</td><td>for Qx Versions</td><td>Description</td></tr></thead>`);
    html.push(`<tbody>`);
    let releases_by_date = {};
    let releases_table = [];
    for (let repo of cache.repos.list) {
        try {
            let data = cache.repos.data[repo];
            if (["(unlisted)", "(deprecated)"].some(txt => (data.description || "").includes(txt))) {
                continue;
            }
            let releases_list = data.releases.list;
            let latest_release = releases_list[releases_list.length-1] || "";
            let repo_html = `<a href="https://github.com/${repo}">${repo}</a>`;
            let latest_release_html = latest_release ? `<a href="https://qooxdoo.org/qxl.packagebrowser/#${repo.replace("/","~")}~library">${latest_release}</a>` : "";
            let release_data = data.releases.data[latest_release];
            let qooxdoo_range = typeof release_data.manifests[0].requires == "object" && release_data.manifests[0].requires['@qooxdoo/framework'];
            if (latest_release && by_date) {
                let published_at = release_data.published_at;
                releases_by_date[published_at] = releases_table.length;
                releases_table.push(`<tr><td>${repo_html}</td><td>${latest_release_html} (${published_at})</td><td>${qooxdoo_range||""}</td><td>${data.description}</td></tr>`);
            } else {
                releases_table.push(`<tr><td>${repo_html}</td><td>${latest_release_html}</td><td>${qooxdoo_range||""}</td><td>${data.description}</td></tr>`);
            }
        } catch (e) {
            console.warn(`${repo}: ${e.message} ${e.stack}`);
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
