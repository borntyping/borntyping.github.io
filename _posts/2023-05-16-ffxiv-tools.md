---
title: Final Fantasy 14 microsites
short: FFXIV microsites
category: Development
layout: post
date: "2023-05-16"
---

Recently I built two small microsites that I find helpful for playing Final Fantasy 14.

* https://borntyping.co.uk/ffxiv-daily-quest-tracker/
* https://borntyping.co.uk/ffxiv-signposts/

While working on a [Backstage]/[React] codebase at [Kaluza] I wanted to take a look at what else the 2023 JavaScript ecosystem had to offer, and especially wanted to experience JavaScript development "from scratch" in a much smaller codebase.

## [ffxiv-daily-quest-tracker]

The first tool I built was a calculator for a series of long quest chains in FFXIV that can only be progressed a small amount each day. I wanted to be able to work out how long each quest chain would take me to finish - being able to visualise my progress kept me a lot more engaged and encouraged me to finish them.

I used [Alpine.js] for this, alongside [Bootstrap]. I was already pretty familiar with Bootstrap, and wanted to build something quite quickly so avoided learning a new CSS framework. [Alpine.js] seemed pretty similar to [htmx], a library I'd had some success with previously for a professional project. I didn't use it here as I wanted to be able to deploy this site to GitHub Pages and avoid the need for a server.

The JavaScript I wrote using Alpine.js was almost certainly not very idiomatic, but it made it very easy to provide some classes containing the structure of my data and then link that into my HTML using `<template>` tags. The two-way binding meant I didn't have to do anything complex to link the fields where a user would provide information to my data model. When the values of those fields change the data model and all the HTML using it immediately updates, even though much of that was in a nested class structure — I didn't need to structure my codebase to fit the conventions of the library like I would have done with React or Vue.

Alpine was very simple to use, and I didn't need to use any build step or dependency management at all, so the end result was very easy to deploy directly to GitHub Pages. The code for the site is ~4 small files (`index.html`, `index.css` for styles, `index.js` for code and `index.json` for data). I'd very happily use Alpine.js again for a website.

## [ffxiv-signposts]

The second site was a list of links to other people's FFXIV sites that I either used or had been recommended. There's a wonderful ecosystem of helpful tools people have built for this game, even though there's not much support from the developers of the game for it (e.g. Destiny 2 provides a very full-featured API with access to information about most things in the game, which has been a great base for developers to build extensive and powerful interfaces to that data). 

This site displayed a long list of cards that each had a link to the site and a list of tags. Each tag had a one-line description alongside it explaining how the site related to the tag. There were also some special tags for "complexity" (how much a player would need to know to use the site) and whether a site was an official site from the developers of the game. A pair of toolbars at the top allow selecting only the cards in a certain category, or tag within that category.

I used [Vue.js] for this, alongside [Bulma]. I wanted to use a framework closer to React that used a component model, so that I could understand the approach better by seeing different ways to implement it. I also wanted to try something different to Bootstrap UI when it came to CSS, as I've very rarely used anything else for a HTML project in a long time.

I was initially attracted to Vue.js for it's promise of being able to work with or without a build step or server, and hoped to take the same approach I did using Alpine.js. That didn't turn out to be very practical, as a lot of it's syntax is only supported via a compilation step. I wanted to look at using [Deno] or [Bun] to manage dependencies and compilation, but I couldn't find enough documentation to bootstrap a working build process — I couldn't find any documentation on how to actually build a Vue.js project, only instructions on how to use `create-vue` to generate all the files I'd need to setup a project with their recommended approach. The development experience and build process using npm and [Vite] was actually pretty good, but it still frustrates me that I've no idea how it works.

Building components with Vue.js was okay. I didn't like the templating language much compared to JSX/TSX, and it was frustrating that I'd need `{brackets}` in some places but not others. I loved that I could write completely normal CSS in a `<style>` tag and have it scoped to the component though, and that was a far nicer experience than the JSS approach I'd previously used in React. Adding animations around changes to the page (e.g. when switching tabs) was incredibly easy using `<TransitionGroup>` with very pleasing results.

I'm not sure I've come out with any strong opinion on using Vue.js in the future — in many ways it felt like a slightly different React, though I think for a good comparison I'd need to use both on similar sized projects. I made very little use of Vue.js' features, especially reactivity which it silently got right without me needing to think about it.

Meanwhile Bulma was a surprisingly good experience. It's a lot smaller in size and scope than Bootstrap, and doesn't come with a full set of components or a JavaScript library. Given that, I expected to be writing far more CSS to extend what it provided, but I actually found myself writing far less CSS than I would in a comparable Bootstrap project. It covered every basic use case I had, and was extremely readable with verbose selectors like `field is-grouped is-grouped-multiline`. This library will probably become the first thing I reach for next time I need a CSS framework.

[Alpine.js]: https://alpinejs.dev/
[Backstage]: https://github.com/backstage/backstage/
[Bootstrap]: https://getbootstrap.com/
[Bulma]: https://bulma.io/
[Bun]: https://bun.sh/
[Deno]: https://deno.com/
[ffxiv-daily-quest-tracker]: https://github.com/borntyping/ffxiv-daily-quest-tracker
[ffxiv-signposts]: https://github.com/borntyping/ffxiv-signposts
[htmx]: https://htmx.org/
[Kaluza]: https://www.kaluza.com/
[React]: https://react.dev/
[Vite]: https://vitejs.dev/
[Vue.js]: https://vuejs.org/
