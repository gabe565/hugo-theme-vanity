# hugo-theme-vanity

<!-- Tagline -->
<p align="center">
    <b>A lightweight and responsive Hugo theme to create vanity URLs for Go packages</b>
    <br />
</p>


<!-- Badges -->
<p align="center">
    <a href="https://github.com/markdumay/hugo-theme-vanity/commits/main" alt="Last commit">
        <img src="https://img.shields.io/github/last-commit/markdumay/hugo-theme-vanity.svg" />
    </a>
    <a href="https://github.com/markdumay/hugo-theme-vanity/issues" alt="Issues">
        <img src="https://img.shields.io/github/issues/markdumay/hugo-theme-vanity.svg" />
    </a>
    <a href="https://github.com/markdumay/hugo-theme-vanity/pulls" alt="Pulls">
        <img src="https://img.shields.io/github/issues-pr-raw/markdumay/hugo-theme-vanity.svg" />
    </a>
    <a href="https://github.com/markdumay/hugo-theme-vanity/blob/main/LICENSE" alt="License">
        <img src="https://img.shields.io/github/license/markdumay/hugo-theme-vanity" />
    </a>
</p>

<!-- Table of Contents -->
<p align="center">
  <a href="#about">About</a> •
  <a href="#prerequisites">Prerequisites</a> •
  <a href="#installation">Installation</a> •
  <a href="#configuration">Configuration</a> •
  <a href="#contributing">Contributing</a> •
  <a href="#donate">Donate</a> •
  <a href="#license">License</a>
</p>


## About
<!-- TODO: Add screenshot -->

Go uses URLs such as `github.com/uber-go/atomic` to import packages. This import statement links directly to the repository hosted on `github.com`. Go supports [vanity import paths][golang_remote_path] to decouple the import path and the code repository. For example, the `atomic` package is made available at `go.uber.org/atomic`, which redirects to GitHub under the hood.

Inspired by the [Uber Go][uber_go_url] landing page, this repository simplifies the creation and maintenance of a website to list and resolve the packages using a vanity base url (e.g. `example.com`). The repository is implemented as a theme called `go-vanity` for [Hugo][hugo_url]. The generated static site can be deployed on any capable host. The next sections describe the prerequisites, installation, and configuration of a vanity site.

<!-- TODO: add tutorial deep-link 
Detailed background information is available on the author's [personal blog][blog].
-->


## Prerequisites
The following prerequisites need to be met in order to use the `go-vanity` theme correctly.
- **A (local) machine with Hugo and Git installed** - Hugo is needed to test the configuration and to generate the static site. The [quickstart][hugo_quickstart] describes the key steps how to get Hugo, including Git, up and running.
- **A web host is required** - A web host is required to host the landing page and the related content generated by Hugo. The [about section][hugo_about] of Hugo displays a list of popular hosting providers.
- **A registered domain name is required** - A domain name (such as `example.com`) is required to be used as basis for the vanity url. The DNS should point to your web host.


## Installation
The `go-vanity` theme can be installed as a regular Hugo theme. Run the following command from within the main directory of your Hugo site.

```console
git submodule add https://github.com/markdumay/hugo-theme-vanity.git themes/go-vanity
```

## Configuration
Once installed, apply the `go-vanity` theme to your main Hugo site in its `config.toml`. The `baseURL` is used as the base path for your vanity URL. Please be aware that Hugo changes this to `localhost:1313` when running locally. Run `hugo server -b http://example.com` to change this behavior. The theme uses one parameter: `redirect`. When `redirect` is set to `false`, individual package URLs will not redirect automatically. This allows you to test the settings and to inspect the generated HTML code. Additionally, a copyright notice is added to the landing page's footer when specified.

```toml
baseURL = "http://example.com/"
languageCode = "en-us"
title = "example.go"
theme = "go-vanity"
copyright = "Copyright © 2021 Author Name; all rights reserved."
[params]
    redirect = true
```

Each package you wish to configure should have its own content file. This file requires two additional variables in the frontmatter: `repository` and `godoc`. The `https://` prefix for these URLs is added  automatically by the `go-vanity` theme. The configuration of `example.com/package` should be defined in `content/package.md`. Lastly, the file should include the tag `package` for the package to be rendered on the landing page.

```yaml
---
title: "package"
date: 2021-09-14T13:20:55+02:00
draft: false
repository: github.com/owner/repo
godoc: pkg.go.dev/example.com/package
tags: [package]
---
```

## Usage
Once configured, run or deploy your Hugo site as usual. When running locally, the landing page is available at `localhost:1313`. The URL `localhost:1313/package` will redirect to `github.com/owner/repo`. When deployed in production, the URLs will change to `example.com` and `example.com/package` respectively. As mentioned in the previous section, setting `redirect` to `false` in the `config.toml` allows you to inspect the generated code for each package.


## Contributing
1. Clone the repository and create a new branch 
    ```console
    $ git checkout https://github.com/markdumay/shelldoc.git -b name_for_new_branch
    ```
2. Make and test the changes
3. Submit a Pull Request with a comprehensive description of the changes


## Credits
The `go-vanity` theme is inspired by the following blog posts and sources:
- Márk Sági-Kazár - [Vanity import paths in Go][mark_sagi_kazar_url]
- Nate Finch - [Vanity Imports with Hugo][nate_finch_vanity_url]
- Uber Go - [Uber's open-source software for Go][uber_go_url]

## Donate
<a href="https://www.buymeacoffee.com/markdumay" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/lato-orange.png" alt="Buy Me A Coffee" style="height: 51px !important;width: 217px !important;"></a>

## License
The `hugo-theme-vanity` codebase is released under the [MIT license][license]. The documentation (including the "README") is licensed under the Creative Commons ([CC BY-NC 4.0)][cc-by-nc-4.0] license.

<!-- MARKDOWN PUBLIC LINKS -->
[cc-by-nc-4.0]: https://creativecommons.org/licenses/by-nc/4.0/
[hugo_url]: https://gohugo.io/
[hugo_about]: https://gohugo.io/about/what-is-hugo/
[hugo_quickstart]: https://gohugo.io/getting-started/quick-start/
[nate_finch_vanity_url]: https://npf.io/2016/10/vanity-imports-with-hugo/
[mark_sagi_kazar_url]: https://sagikazarmark.hu/blog/vanity-import-paths-in-go/
[golang_remote_path]: https://golang.org/cmd/go/#hdr-Remote_import_paths
[uber_go_url]: http://go.uber.org

<!-- MARKDOWN MAINTAINED LINKS -->
<!-- TODO: add blog link
[blog]: https://markdumay.com
-->
[blog]: https://github.com/markdumay
[license]: https://github.com/markdumay/hugo-theme-vanity/blob/main/LICENSE
[repository]: https://github.com/markdumay/hugo-theme-vanity.git