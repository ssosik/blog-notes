---
title: Rolling my own Vim Markdown plugin
description: Writing a Markdown Diary Vim plugin with Xapian indexing and FrontMatter metadata
lead: ""
date: "2019-03-11T11:22:00-04:00"
lastmod: "2019-03-11T11:22:00-04:00"
tags:
  - vimwiki
  - vim
draft: false
weight: 50
images: []
contributors:
  - steve
---

I've been bumping into the hard edges of Vimwiki too much, so I've decided to
try to roll my own Vim plugin. Vim supports plugins written in Python3, which is
a huge plus.

http://candidtim.github.io/vim/2017/08/11/write-vim-plugin-in-python.html

On my Debian box I needed to `apt-get install vim-nox` in order to get Python3
support added to Vim.

Leveraging Vim's default file template, I can have a blank Markdown template
that includes all of the Metadata/Frontmatter fields that I'll need in order to
use the **gatsby-material-starter** builder.

This plugin should offer these features:

- Ability to author new docs with some prepopulated fields:
    - date
    - author
    - filename
    - date
    - etc
- Index each markdown file in a Xapian DB to enable efficient and effective text
  search. Most importantly:
    - tags search based on the tags field in document Metadata
- Using Xapian queries, generate index pages sorted by date descending, with
  links to each file based on the document **title** metadata field
- Port over the nice features from Vimwiki:
    - keybindings
    - calendar
    - checklists
    - links to arbitrarily named files, separately structured data
    - multiple distinct wikis (i.e. work, public, private)
