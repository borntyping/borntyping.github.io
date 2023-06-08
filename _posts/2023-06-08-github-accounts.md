---
title: Why I have separate personal and work GitHub accounts
short: Separate work GitHub account
category: Development
layout: post
date: "2023-05-16"
---

Permissions on a GitHub token are opt-in for an organisation, but you can't opt out of granting permissions for the account the token belongs to.
For instance, if an GitHub App or GitHub OAuth application at my place of work requests permissions to read private repositories (a very common permission needed for basic actions like cloning), the token issued at the end of the authentication flow will always have permissions to access my personal respositories.
Depending on the settings of the organisation, this may be automatically granted, or may require going though the single-sign on process for that organisation before the token is granted permissions to read from private repositories in the organisation.

If I use the same account for both personal use of GitHub and work use of GitHub, that restricts how carefully I can control access to resources owned by my account.
A particually relevant example of this was the recent [CircleCI breach], which was the event that prompted me to start using two GitHub accounts.
If my account was used purely for personal use, I could have happily removed the application from my account and not worried about it again.
But, since my job required working with CircleCI I needed to stay authenticated to it and take the risk that any access tokens were still vulnerable after beeing rotated.

I also work a lot on developer tooling, which means issuing a lot of tokens to work on GitHub applications locally.
These are subject to much the same problems, and importantly, end up on devices that you don't own and may get used with unfinished or insecure code.

My GitHub account was created well over a decade ago now - it's older than most of the companies I work for, and while the risks here are extremely low I'm a lot more comfortable taking the approach of having a less-valuable GitHub account dedicated to corporate use rather than using something that's been a very public part of my online presense for a long time.

There have been some other advantages to this split.
I use separate mobile phones for personal use and work use, and this means I can use the GitHub android app without needing to go though corportate SSO on a personal device, or getting work-related GitHub notifcations while I'm not working.
It's also nice to have separate GitHub contribution graphs for my own personal work and corportate work.

You can find me on GitHub at [@borntyping] and [@borntyping-corporate].

[@borntyping-corporate]: https://github.com/borntyping-corporate
[@borntyping]: https://github.com/borntyping
[CircleCI breach]: https://circleci.com/blog/jan-4-2023-incident-report/
