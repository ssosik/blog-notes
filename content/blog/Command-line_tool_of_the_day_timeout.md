---
title: Command-line tool of the day timeout
description: ""
lead: ""
date: "2019-02-28T14:30:00-05:00"
lastmod: "2019-02-28T14:30:00-05:00"
tags:
  - bash
  - blog
draft: false
weight: 50
images: []
contributors:
  - steve
---

Use `timeout` to run a command for set amount of time. I'm using it to
temporarily swap out a running service for a spoofed service to see how
this disruption effects a consumer of this service:

    while true ; do
       sleep $(echo "$RANDOM / 1000" | bc)
       date
       <stop real service>
       timeout 60 <spoof service binary>
       <restart real service>
    done

I can let this test bake for a long time, then come back later and
scrape the logs to verify the consumer of this service handled the
errors correctly.
