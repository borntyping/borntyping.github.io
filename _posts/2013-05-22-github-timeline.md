---
title: Playing with the Github Timeline data
summary: Finding accurate counts for GitHub contributions by language
category: Development
layout: post
---

I came across ['The Open Source Report Card'](http://osrc.dfm.io/) today, which included some interesting results on [my report](http://osrc.dfm.io/borntyping). It claimed I'd contributed to repositories using `VimL` and `Go`, neither of which I could remember doing anything in relation to.

Looking into how it worked led to the [Github Archive](http://www.githubarchive.org/), which is available as a dataset on [Google BigQuery](https://bigquery.cloud.google.com/). Playing with this eventually led to finding the problem - the 'contributions' graph included *all* of a users events. This included 'star' (previously 'follow') events, so it was counting repositories I'd starred as repositories that I had contributed to.

A more accurate result was achieved with the following query:

```sql
    /* Count the number of my events by language excluding stars/follows */

    SELECT repository_language, count(repository_language) as n,
    FROM [githubarchive:github.timeline]
    WHERE actor="borntyping" AND type != "WatchEvent"
    GROUP BY repository_language
    ORDER BY n DESC
```

The Github Archive documentation seemed to be devoid of simpler example queries, so this is how I reached the above one, starting from one adapted from the primary example on [githubarchive.org](http://www.githubarchive.org/).

```sql
    /* List all of my repositories, counting the number of events */

    SELECT repository_name, repository_owner, count(repository_name) as events,
    FROM [githubarchive:github.timeline]
    WHERE repository_owner="borntyping"
    GROUP BY repository_name, repository_owner
    ORDER BY events DESC

    /* List all of my repositories, counting the number of events, and sorted by language */

    SELECT repository_name, repository_owner, repository_language, count(repository_name) as events,
    FROM [githubarchive:github.timeline]
    WHERE actor="borntyping"
    GROUP BY repository_name, repository_owner, repository_language
    ORDER BY repository_language, events DESC

    /* Count the number of my events by language */

    SELECT repository_language, count(repository_language) as repository_language_count,
    FROM [githubarchive:github.timeline]
    WHERE actor="borntyping"
    GROUP BY repository_language
    ORDER BY repository_language_count DESC
```
