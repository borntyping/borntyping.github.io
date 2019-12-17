---
layout: page
title: About me
---

I am Sam Clements - a programmer, open-sourcerer, and game master.

You can contact me by email at [sam@borntyping.co.uk][email] or on Twitter at [@borntyping][twitter].

## Professional work

I currently work as an _Automation Engineer_ doing Python developement at [InfoSum][is].
I've previously worked as a *IT Consultant* doing Python development at [General Bioinformatics][gb]
and as an *Operations Engineer* doing Ruby development at [DataSift][ds].
I studied *Open Source Computing* at [Aberystwyth University][au].
I generally work on "DevOps" projects, writing code in Python, Ruby, Bash and other languages to automate data and software release processes.

You can contact me as [Sam Clements][linkedin] on LinkedIn.

## Open source work

I list some of my open source projects and contributions on the [Open source projects]({{ site.baseurl }}/open-source/) page on this site.
I mostly build small tools and applications written in Python, usually to support development or systems adminstration workflows.

My projects are published under [@borntyping][github] and [@borntyping-sandbox][github-sandbox] on GitHub and under [@borntyping][gitlab] on GitLab.

## Pages

<ul class="related-posts">
{% for node in site.pages %}{% if node.title != null %}{% if node.layout == "page" %}
  <li><h3><a href="{{ node.url }}">{{ node.title }}</a></h3></li>
{% endif %}{% endif %}{% endfor %}
</ul>

## Posts

I occasionally write about programming, package management, and D&D.

<ul class="related-posts">
{% for post in site.posts %}
  <li>
    <h3>
      <a href="{{ post.url }}">
        {{ post.title }}
        <small>{{ post.date | date_to_string }}</small>
      </a>
    </h3>
  </li>
{% endfor %}
</ul>

[au]: http://www.aber.ac.uk/en/
[dm]: https://en.wikipedia.org/wiki/Dungeon_Master
[ds]: http://datasift.com/
[gb]: https://www.generalbioinformatics.com/
[is]: https://www.infosum.com/

[github]: https://github.com/borntyping/
[github-sandbox]: https://github.com/borntyping-sandbox/
[gitlab]: https://gitlab.com/borntyping/
[email]: mailto:sam@borntyping.co.uk
[twitter]: https://twitter.com/borntyping
[linkedin]: https://www.linkedin.com/in/borntyping/
