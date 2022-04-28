# Welcome to the Hugo documentation templater

This guide shows you how to use this templater to create a Converged Cloud technical documentation site.

## Create a new documentation site from scratch

### Install Hugo extended version

#### Mac users

```
brew install hugo
```

To verify your new install:

```
hugo version
```

### Create a Hugo site

```
hugo new site my-docu-site
cd  my-docu-site
```

### Turn your site into a Hugo Module

```
  hugo mod init github.com/cc/my-docu-site
```

### Declare the hugo-documentation-templater module as a dependency for your site

Normally you would add the module as following:

```
hugo mod get github.com/sapcc/hugo-documentation-templater
```

But if you are developing this module add the following config to the go.mod file and it will redirect to your local folder:

```
module github.com/me/my-docu-site

// just for local dev!
replace github.wdf.sap.corp/cc/hugo-documentation-templater => /Users/d063222/Documents/sap/monsoon/hugo-documentation-templater

go 1.17

require github.com/sapcc/hugo-documentation-templater v0.0.0-somegiberish // indirect
```

### Edit the Hugo config file `config.yaml` (originally is `config.toml` but I prefer yaml) as following to import the templater:

```
baseURL: "http://example.org/"
languageCode: "en-us"
title: "My New SAP CC Doc Site"

module:
  hugoVersion:
    extended: true
    min: 0.73.0
  imports:
    - path: github.com/sapcc/hugo-documentation-templater
      disable: false
```

## Content and Customization

### Site name

Edit the name attribute on the Hugo config file `config.yaml`.

### Add Non-content Entries to a Menu

Add a menu configuration similar to the following in the `config.yaml` (see [Hugo documentation](https://gohugo.io/content-management/menus/)):

```
menu:
  main:
    - identifier: "Home"
      name: "Home"
      pre: "<i class='fas fa-home'></i>"
      url: "/"
      weight: 100
```

### Landing page

Add a file named `_index.md` to the root of content folder with following content to customize the landing page:

```
---
heroTitle: "The best documentation ever"
heroSubtitle: "This is the subtitle of the hero section"
---
```

### Landing page with custom section index to jump to specific documentation sections

Add this parameter `landingSectionIndex: true` to the `_index.md` file of the desired section or markdown file.

Example:
Given an architecture folder with the section definition file `content/docs/architecture/_index.md` with parameter `landingSectionIndex: true` as following:

```
---
title: "Architecture"
linkTitle: "Architecture"
weight: 1
landingSectionIndex: true
description: >
  Architecture overview
---
```

A new entry will be created in the section at the bottom of the landing page with links and descriptions to jump directly to the desired sections.

### Documentation

Just drop your documnentation well organized in folders under `content/docs/`. Each folder should contain a `_index.md` file containing following information:

```
---
title: "Main title of the section"
linkTitle: "Name on the side navigation"
weight: "integer number describing the position in the side bar"
description: >
  "Some description useful"
---
```

## Extra information

### Bootstrap version

Based on Bootstrap 4.6

### Buil assets

Creating a new package.json file
https://docs.npmjs.com/creating-a-package-json-file

Install PostCSS so that the site build can create the final CSS assets
https://github.com/google/docsy#prerequisites
