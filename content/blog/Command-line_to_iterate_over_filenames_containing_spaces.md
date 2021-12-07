---
title: Command-line to iterate over filenames containing spaces
description: ""
lead: ""
date: "2019-03-03T19:40:00-05:00"
lastmod: "2019-03-03T19:40:00-05:00"
tags:
  - bash
  - blog
draft: false
weight: 50
images: []
contributors:
  - steve
---

Command line tools are pretty powerful, but there are some edge cases
that take some extra care. For example, using a `for` loop over a set of
files can be really useful, but if those filenames contain a space then
things may not work as expected.

So here's a quick recipe to work around this problem.

What would normally be something like:

``` {.bash}
for F in $(find . -type f -name "*.wiki") ; do
    <do stuff>
done
```

This falls down when the filenames contain one or more spaces, since the
for-loop iterates on whitespace-delimited tokens in the list.

Instead, do something like this:

``` {.bash}
while read F ; do
    <do stuff>
done < <(find . -type f -name '*.wiki')
```

TODO explain why/how this works
