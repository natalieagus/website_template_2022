# Course Site Template 2022

This repository contains website template suitable to host course notes and handouts. Currently, it's populated with materials from CSE 50.005 as example.

## General setup

### Installation

This website is built using Jekyll. You can get it installed by [reading this guide](https://jekyllrb.com/docs/installation/). Afterwards, install the jekyll and bundler gems, and serve:

```
gem install jekyll bundler
bundle exec jekyll serve
```

You can then browse to localhost: http://127.0.0.1:4000

### `_config.yml`

Important parts to edit:

1. `url`: the site the website is hosted on
2. `baseurl`: the route to reach the `home` of the website, e.g: repo name if it's Github Pages
3. `title` and `description`
4. `collections`: directories containing markdown files that will be processed by `jekyll`. Omit the `_`.

### Creating Content

Jekyll will process any `.md` files inside any directories stated under `collections` in `_config.yml`. The name must start with an `_`. To **add** a new content, create **markdown** files in any of the folders named `_[collection_name]`.

For example we have:

- `_os_notes`
- `_ns_notes`
- `_assignments`
- `_ns_labs`
- `_os_labs`

Use the **front matter** template as given in the sample `*.md` files inside each of the directory. For instance. The layout is recommended to be `article`, and you can choose the title of the `sidebar nav` as what is stated in `_data/navigation.yml`. `Aside toc` is also recommended (right side table of content).

```
---
title: Introduction to OS
permalink: /os_notes/week1_intro
key: os-notes-week1_intro
layout: article
nav_key: os_notes
sidebar:
  nav: os_notes
license: false
aside:
  toc: true
show_edit_on_github: false
show_date: false
---
```

### Adding sidebar navigation (left navigation bar)

If your `.md` page uses `sidebar nav` option then edit `_data/navigation.yml`. You can set the sidebar nav to look like anything you want by matching its `url` key with each `.md` page's `permalink`.

Note that the **sidebar-nav** and **nav-key** in the front matter of the new `.md` file must match the name you declare in this navigation yaml file. For instance, `os_notes` sidenav will be shown when you're at the page `/os_notes/week1_intro` above.

```
os_notes:
  - title: Basics of OS
    children:
      - title: Introduction to OS
        url: /os_notes/week1_intro
      - title: The Kernel
        url: /os_notes/week1_kernel
      - title: Resource Allocator and Coordinator
        url: /os_notes/week1_resource
      - title: Memory and Process Management
        url: /os_notes/week1_mpm
```

## Aesthetics

Replace the .svg file inside `/_includes/svg/logo.svg` with the same name.

### Custom CSS

Add any custom sass styling in `/_sass/custom.scss`

### Changing Favicon

Replace `assets/favicon.ico` with your file named `favicon.ico` as well

### Custom html for articles

Add any additional elements in `/_includes/article/footer/custom.html`. You may also add it at `/_includes/article/top/custom.html` if you want it to execute first.
Current added features:

- Go to top button at `/_includes/article/top/custom.html`
- Collapsible answer box at `/_includes/article/footer/custom.html`
- All styling in `custom.scss`

## Useful Snippets and Shortcuts

### Markdown Snippets

It's useful to add HTML snippets if you're using VSCode, for instance:

````json
{
  "Highlight code": {
    "prefix": "highlight",
    "body": [
      "<span style=\"background-color:yellow; color: black\">$TM_SELECTED_TEXT${1:}</span>"
    ],
    "description": "highlight selected text"
  },

  "Custom box": {
    "prefix": "box",
    "body": [
      "<div class=\"$1\"><div class=\"custom_box\">$TM_SELECTED_TEXT$2 </div></div><br>"
    ],
    "description": "custom box"
  },
  "Code block": {
    "prefix": "codeblock",
    "body": ["```java\n$TM_SELECTED_TEXT${1:}\n```"],
    "description": "custom code block"
  },
  "Image block": {
    "prefix": "imageblock",
    "body": [
      "<img src=\"{{ site.baseurl }}$1\"  class=\"center_seventy$2\"/>$3"
    ],
    "description": "custom image block"
  },
  "Image vanilla block": {
    "prefix": "imageblock",
    "body": ["<img src=\"$1\" />$2"],
    "description": "custom image block"
  },
  "Red block": {
    "prefix": "redwords",
    "body": [
      "<span style=\"color:#f7007f;\"><b>$TM_SELECTED_TEXT$1</b></span>"
    ],
    "description": "custom redword block"
  },
  "Yellow block": {
    "prefix": "yellowords",
    "body": [
      "<span style=\"color:#f77729;\"><b>$TM_SELECTED_TEXT$1</b></span>"
    ],
    "description": "custom yellow block"
  },
  "Video block": {
    "prefix": "videoblock",
    "body": [
      "<video width =\"100%\" height = \"100%\" controls=\"controls\" preload=\"metadata\" src=\"$1#t=0.5\"> Your browser does not support the HTML5 Video element.</video>$2"
    ],
    "description": "custom video block"
  },
  "Task block": {
    "prefix": "taskblock",
    "body": ["### Task $1 $2`TASK $3:`{:.info} $4"],
    "description": "custom task block"
  },
  "Break line": {
    "prefix": "breakline",
    "body": ["<br>"],
    "description": "custom breakline"
  }
}
````

### Shortcuts

...and then bind them with keyboard shortcuts:

```json
{
    "key": "ctrl+alt+c",
    "command": "editor.action.insertSnippet",
    "args": { "name": "Highlight code" },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
  {
    "key": "ctrl+alt+u",
    "command": "editor.action.insertSnippet",
    "args": { "name": "Custom box" },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
  {
    "key": "ctrl+alt+n",
    "command": "editor.action.insertSnippet",
    "args": { "name": "Code block" },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
  {
    "key": "ctrl+alt+m",
    "command": "editor.action.insertSnippet",
    "args": { "name": "Image block" },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
  {
    "key": "ctrl+alt+,",
    "command": "editor.action.insertSnippet",
    "args": { "name": "Video block" },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
  {
    "key": "ctrl+alt+.",
    "command": "editor.action.insertSnippet",
    "args": { "name": "Image vanilla block" },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
  {
    "key": "ctrl+alt+r",
    "command": "editor.action.insertSnippet",
    "args": { "name": "Red block" },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
  {
    "key": "ctrl+b",
    "command": "editor.action.insertSnippet",
    "args": { "name": "Yellow block" },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
  {
    "key": "ctrl+alt+t",
    "command": "editor.action.insertSnippet",
    "args": { "name": "Task block" },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
```

### Paste Image

To paste images conveniently, the extension [Paste Image](https://marketplace.visualstudio.com/items?itemName=mushan.vscode-paste-image) and [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) are particularly useful.

The settings that I use for Paste Image in my project is:

```
  "pasteImage.path": "${projectRoot}/assets/images/${currentFileNameWithoutExt}",
  "pasteImage.basePath": "${projectRoot}",
  "pasteImage.forceUnixStyleSeparator": true,
  "pasteImage.prefix": "/", // change this if we have projects that require baseURL
  "pasteImage.insertPattern": "${imageFilePath}",
```

and it's bound to the shortcut:

```
  {
    "key": "ctrl+alt+v",
    "command": "extension.pasteImage",
    "when": "editorTextFocus"
  },
```
