---
title: A Makefile to build markdown
description: ""
lead: ""
date: "2019-03-19T17:13:42-04:00"
lastmod: "2019-03-19T17:13:42-04:00"
tags:
  - make
  - pandoc
  - blog
draft: false
weight: 50
images: []
contributors:
  - steve
---

I ended up not using this, but saving it here for posterity in case I
want to reference it later on.

My thinking was that I'd have bare markdown files that were managed with
the Vimwiki plugin. I would then run make to add in the `frontmatter`
data to make the files usable in gatsby:

    # Idea taken from https://gist.github.com/kristopherjohnson/7466917#file-makefile

    # To handle files that contain ':' colons properly, escape the colons in the
    # SOURCE_DOCS variable.
    SOURCE_DOCS := $(subst :,\:,$(wildcard *.md))
    EXPORTED_DOCS=$(SOURCE_DOCS:.md=.markdown)

    PANDOC=/usr/bin/pandoc
    RM=/bin/rm

    PANDOC_OPTIONS=--standalone --from markdown+yaml_metadata_block --to markdown+yaml_metadata_block --atx-headers

    # Pattern-matching Rules

    %.markdown : %.md
           TITLE=$$(head -n 10 $< | grep '^# ' | head -n +1 | tr -d '#'); \
           DATE=$$(basename -s .md $< | tr '_' ' ' | sed  's/\(.*\)/"\1"/' | xargs date --iso-8601=seconds -d); \
           TAGS=$$(grep '^:[^[:space:]]\+:$$' $< | tr ':' ' '); \
           $(PANDOC) $(PANDOC_OPTIONS) -M title:"$$TITLE" -M date:"$$DATE" -M tags:"$$TAGS" -o $@ $<; \
           sed -i '/^:[^[:space:]]\+:$$/d' $@

    all : $(EXPORTED_DOCS)

    clean:
           - $(RM) $(EXPORTED_DOCS)
