---
layout: page
theme: theme-base-0d
---

Hi! I'm Sam Clements.

You can find me on Mastodon at [@borntyping@hachyderm.io](https://hachyderm.io/@borntyping) or email me at  [sam@borntyping.co.uk](mailto:sam@borntyping.co.uk).

I use this site to publish a list of [books I recommend]({% link books.md %}) and occasionally write [blog posts](#posts) about things I've been working on.

## Professional work

You can find me at [Sam Clements][linkedin] on LinkedIn.

I've spent my career building tools and processes for people that run software.
I've worked in teams labeled "operations", "devops", "infrastructure", "developer experience", and "platform engineering"; always with the goal of making things easier for my co-workers.

I'm at my best when working on tools for other engineers, and have broad experience across projects that have included complex CI/CD pipelines, web applications, REST APIs, infrastructure-as-code, dependency and release management services, and automated test suites.

I'm an expert Python programmer, and pick up languages like Golang, JavaScript, TypeScript, PHP, Rust, Java, and Ruby as and when I need to.

* Software Engineer (Linode Object Storage) at [Akamai][akamai] (2024–)
* Production Engineer (Developer Experience) at [Kaluza][kaluza] (2022–2023)
* Senior DevOps Engineer at [Datto][datto] (2021–2022)
* Automation Engineer at [InfoSum][infosum] (2018–2021)
* IT Consultant at [General Bioinformatics][general-bioinformatics] (2017–2018)
* Operations Engineer at [DataSift][datasift] (2013–2017)
* Studied *Open Source Computing* at [Aberystwyth University][au] (2011–2015)

## Open source work

You can find me at [@borntyping][github] on GitHub and at [@borntyping][gitlab] on GitLab.

I list some of my open source projects and contributions on the [Open source projects]({% link open-source.md %}) page on this site.

Most of the useful projects are small Python libraries or applications that aim to "do one thing well". Some highlights:

- [Switchbox][switchbox] — automation of some personal git workflows (2022)
- [simple_logger][simple_logger] — an easy to configure Rust logger (2015)
- [rust-psutil][rust-psutil] - process and system info library (2015)
- [dice][dice] — a CLI and Python library for parsing and evaluating dice notation (2013)
- [colorlog][simple_logger] — a popular Python logging formatter (2012)

I've recently been working on some tiny web-apps for myself:

- [Vancelle] — a personal media catalogue (2024)
- [FFXIV Timers][ffxiv-timers] — a clock for game events (2023)
- [FFXIV Signposts][ffxiv-signposts] — a list of FFXIV resources (2023)
- [FFXIV Daily Quest Tracker][ffxiv-daily-quest-tracker] — a calculator for daily tasks (2023)

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
[akamai]: https://www.akamai.com/

[github]: https://github.com/borntyping/
[github-sandbox]: https://github.com/borntyping-sandbox/
[gitlab]: https://gitlab.com/borntyping/
[linkedin]: https://www.linkedin.com/in/borntyping/
[cohost]: https://cohost.org/borntyping

[ffxiv-timers]: https://borntyping.co.uk/ffxiv-timers/
[ffxiv-signposts]: https://borntyping.co.uk/ffxiv-signposts/
[ffxiv-daily-quest-tracker]: https://borntyping.co.uk/ffxiv-daily-quest-tracker/
[switchbox]: https://github.com/borntyping/switchbox
[simple_logger]: https://github.com/borntyping/rust-simple_logger
[dice]: https://github.com/borntyping/python-dice
[Vancelle]: https://github.com/borntyping/vancelle
[rust-psutil]: https://github.com/rust-psutil/rust-psutil/
