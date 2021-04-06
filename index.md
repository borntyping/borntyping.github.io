---
layout: page
---

I am Sam Clements - a programmer, operator, and open-sourcerer.

You can contact me by email at [sam@borntyping.co.uk][email] or on Twitter at [@borntyping][twitter].

## Professional work

I work on "DevOps" projects, writing code to automate data and software release processes.
I usually build applications in Python, but have also written and published code using Rust, Ruby and Bash.

* _2021-present_ DevOps Engineer II at [Datto][dt]
* _2018-2021_ Automation Engineer at [InfoSum][is]
* _2017-2018_ IT Consultant at [General Bioinformatics][gb]
* _2013-2017_ Operations Engineer at [DataSift][ds]
* _2011-2015_ Studied *Open Source Computing* at [Aberystwyth University][au]

You can contact me as [Sam Clements][linkedin] on LinkedIn.

## Open source work

I list some of my open source projects and contributions on the [Open source projects]({{ site.baseurl }}/open-source/) page on this site.
I mostly build small tools and applications written in Python, usually to support development or systems adminstration workflows.

My projects are published under [@borntyping][github] on GitHub and under [@borntyping][gitlab] on GitLab.

## Pages

<ul class="related-posts">
{% for node in site.pages %}
{% if node.layout == "page" && node.title != null %}
  <li><a href="{{ node.url }}">{{ node.title }}</a></li>
{% endif %}
{% endfor %}
</ul>

## Posts

I occasionally write about programming, package management, and D&D.

<ul class="related-posts">
{% for post in site.posts %}
  <li>
    <a href="{{ post.url }}">
      {{ post.title }}
      <small>{{ post.date | date_to_string }}</small>
    </a>
  </li>
{% endfor %}
</ul>

[au]: http://www.aber.ac.uk/en/
[dm]: https://en.wikipedia.org/wiki/Dungeon_Master
[ds]: http://datasift.com/
[gb]: https://www.generalbioinformatics.com/
[is]: https://www.infosum.com/
[dt]: https://www.datto.com/

[github]: https://github.com/borntyping/
[github-sandbox]: https://github.com/borntyping-sandbox/
[gitlab]: https://gitlab.com/borntyping/
[email]: mailto:sam@borntyping.co.uk
[twitter]: https://twitter.com/borntyping
[linkedin]: https://www.linkedin.com/in/borntyping/
