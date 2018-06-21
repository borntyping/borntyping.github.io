---
layout: post
title: Package versioning
---

This post descibes my approach to versioning packaged applications, using version numbers that look like this: `3.2.0-2109.12272`.

The first part (`3.2.0`) is a **manually incremented version number**. It's incremented for changes that need to be communicated and talked about - "our new feature will be in version 4, which will be deployed next week".

The second part (`2109.12272`) is an **automatically incremented release number**. It's entirely managed by the CI/CD process that packages the software. In my case, that's done using GitLab, and the number is composed from the pipeline and job identifiers.

Both of these numbers increase monotonically, so that a each time the CI/CD process runs it builds a package with a higher version and release number without a human needing to remember to manually increase it. The automatic release number also ensures that you never build a package with the same version number as an existing one, and so as long as you keep older packages around you can always downgrade to a previous version.

The approach works very neatly with packaging tools like RPM, which have seperate version and release fields. My build process uses a `version.txt` and `release.txt` file, the latter of which is created at build time. Both are included in the package name and in the package itself, allowing the application to read them at runtime to display it's own version number.

You could quite easily remove the manually incremented version number and loose no technical capability. However, I find simple, easy to remember numbers much easier to communicate than the long digit sequences an automatic release number will provide. Asking someone to check if they are running "version 4 or above" is much simpler than asking if the version number is "12034 or above" - people remember small numbers much more easily. You can also still use familiar [SemVer](https://semver.org/) like semantics to describe the scale of change - "we're upgrading from version 9034 to 9725" says very little about the changes involved, whereas "we're upgading from version 4.1 to 5.3" implies multiple large changes, or "we're upgading from version 4.1.0 to 4.1.1" implies a small fix. I find this is especially useful when communicating with non-technical people who use the application.

However, a downside to this is that humans will likely end up being very lax about changing the version number. This is fine for me - I only use it to commuicate major changes and not small patches - but is unlikely to work for all cases. It's particually unsuited for libraries or APIs, where tracking API changes is important and strictly following [SemVer](https://semver.org/) may be important.
