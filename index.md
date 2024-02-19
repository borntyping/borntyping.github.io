---
layout: page
theme: theme-base-0d
---

Hi! I'm Sam Clements.

You can contact me by email at [sam@borntyping.co.uk][email].

## Professional work

I'm a software engineer with a history of developing internal tooling for engineering teams. I've worked in teams labeled "devops", "operations", "infrastructure", and "developer experience"; but always with the goal of making my peers more effective.

I'm at my best when working on tools for other engineers, and have broad experience across projects that have included complex CI/CD pipelines, web applications, REST APIs, dependency and release management services, infrastructure-as-code deployments, and automated test suites.

I'm an expert Python programmer, and pick up languages like JavaScript, TypeScript, PHP, Rust, Java, and Ruby as and when I need to.

* Production Engineer at [Kaluza][kaluza] (2022–2023)
* Senior DevOps Engineer at [Datto][datto] (2021–2022)
* Automation Engineer at [InfoSum][infosum] (2018–2021)
* IT Consultant at [General Bioinformatics][general-bioinformatics] (2017–2018)
* Operations Engineer at [DataSift][datasift] (2013–2017)
* Studied *Open Source Computing* at [Aberystwyth University][au] (2011–2015)

You can contact me as [Sam Clements][linkedin] on LinkedIn.

## Open source work

You can find me at [@borntyping][github] on GitHub and at [@borntyping][gitlab] on GitLab.

I list some of my open source projects and contributions on the [Open source projects][open-source] page on this site.

Most of the useful projects are small Python libraries or applications that aim to "do one thing well". Some highlights:

- [Vancelle] — a personal media catalogue (2024)
- [Switchbox][switchbox] — automation of some personal git workflows (2022)
- [simple_logger][simple_logger] — an easy to configure Rust logger (2015–ongoing)
- [dice][dice] — a CLI and Python library for parsing and evaluating dice notation (2013)
- [colorlog][simple_logger] — a popular Python logging formatter (2012–ongoing)

I've recently been working on some tiny web-apps for Final Fantasy 14:

- [FFXIV Timers][ffxiv-timers] — a tiny web app using with [Svelte](https://svelte.dev/).
- [FFXIV Signposts][ffxiv-signposts] — a tiny web app using [Vue.js](https://vuejs.org) (2023)
- [FFXIV Daily Quest Tracker][ffxiv-daily-quest-tracker] — a tiny web app using [Alpine.js](https://alpinejs.dev/) (2023)

## Personal life

I also use this site to publish a list of [books I recommend][books], containing some of my favourite works of fiction.

You can find me at [@borntyping][cohost] on cohost.

## Posts

<ul class="related-posts">
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">
        {{ post.title }}
        <small>{{ post.category }}, {{ post.date | date_to_string }}</small>
      </a>
    </li>
  {% endfor %}
</ul>

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
[linkedin]: https://www.linkedin.com/in/borntyping/
[cohost]: https://cohost.org/borntyping

[ffxiv-timers]: https://borntyping.co.uk/ffxiv-timers/
[ffxiv-signposts]: https://borntyping.co.uk/ffxiv-signposts/
[ffxiv-daily-quest-tracker]: https://borntyping.co.uk/ffxiv-daily-quest-tracker/
[switchbox]: https://github.com/borntyping/switchbox
[simple_logger]: https://github.com/borntyping/rust-simple_logger
[dice]: https://github.com/borntyping/python-dice
[Vancelle]: https://github.com/borntyping/vancelle

[books]: {% link books.md %}
[open-source]: {% link open-source.md %}
