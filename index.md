---
layout: page
---

Hi! I'm Sam Clements. I'm currently working as a Production Engineer at [Kaluza][kaluza].

You can contact me by email at [sam@borntyping.co.uk][email].

## Professional work

I'm a a software engineer with a career of working across the spectrum of Operations, DevOps, and SRE roles.

I'm most effective when working on release pipelines, but have broad experience across projects that have included REST APIs, automated test suites for web applications and APIs, dependency and release management services, and large infrastructure-as-code deployments.

I'm an expert Python programmer, and pick up languages like PHP, Rust, Java, and Ruby as and when I need to.

* _2022-present_ DevOps Engineer II at [Kaluza][kaluza]
* _2021-2022_ Senior DevOps Engineer at [Datto][datto]
* _2018-2021_ Automation Engineer at [InfoSum][infosum]
* _2017-2018_ IT Consultant at [General Bioinformatics][general-bioinformatics]
* _2013-2017_ Operations Engineer at [DataSift][datasift]
* _2011-2015_ Studied *Open Source Computing* at [Aberystwyth University][au]

You can contact me as [Sam Clements][linkedin] on LinkedIn.

## Open source work

I list some of my open source projects and contributions on the [Open source projects][open-source] page on this site.

Most of the useful projects are small Python libraries or command line applications that aim to "do one thing well".

You can find me at [@borntyping][github] on GitHub and at [@borntyping][gitlab] on GitLab.

## Personal life

I also use this site to publish a list of [books I recommend][books], containing some of my favourite works of fiction.

## Posts

<nav>
  {% for category in src_ordered_categories %}
    <h3>{{ site.categories[category][0] }}</h3>
    <ul class="related-posts">
      {% for post in site.categories[category][1] %}
        <li>
          <a href="{{ post.url }}">
            {{ post.title }}
            <small>{{ post.date | date_to_string }}</small>
          </a>
        </li>
      {% endfor %}
    </ul>
  {% endfor %}
</nav>

[au]: http://www.aber.ac.uk/en/
[datasift]: http://datasift.com/
[general-bioinformatics]: https://www.generalbioinformatics.com/
[infosum]: https://www.infosum.com/
[datto]: https://www.datto.com/
[kaluza]: https://www.kaluza.com/

[github]: https://github.com/borntyping/
[github-sandbox]: https://github.com/borntyping-sandbox/
[gitlab]: https://gitlab.com/borntyping/
[email]: mailto:sam@borntyping.co.uk
[twitter]: https://twitter.com/borntyping
[linkedin]: https://www.linkedin.com/in/borntyping/

[books]: {% link books.md %}
[open-source]: {% link open-source.md %}
