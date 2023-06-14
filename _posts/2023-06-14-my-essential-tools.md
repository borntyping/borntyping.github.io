---
title: My essential tools
category: Development
layout: post
date: "2023-06-14"
---

A common theme across the tools I use frequently is that they all let me do work faster or with less repetition. I thought I'd list the tools I use a lot and wouldn't want to go without when doing software development.

I've spent a lot of time installing, configuring, and managing my toolkit — probably more time than I've saved! However, even if I've not saved any time, I find it a lot easier to both focus and get things right when I can automate something. It's very easy to make mistakes with repetitive tasks, especially if you have to remember a lot of details that aren't relevant to your current goal.

### Development

These are the tools I use constantly when working on code.

- **[PyCharm Professional](https://www.jetbrains.com/pycharm/)**, **[Visual Studio Code](https://code.visualstudio.com/)**, and **[Micro](https://micro-editor.github.io/)**. I use PyCharm by default as JetBrains code intelligence tools greatly improve my productivity on most codebases. Just being able to quickly (and reliably) jump to definitions or usages is enough to make this my favorite editor. I use VSCode or Micro when I want to edit something quickly.
- **[Git Cola](https://git-cola.github.io/)**. A very simple GUI for Git. I use it write commit messages and preview the changes that will be included in a commit.
- **[Switchbox](https://github.com/borntyping/switchbox)**. My personal git toolbox, used to automate repetitive branch management tasks like rebasing and cleaning up merged branches.
- **[Fedora](https://fedoraproject.org/)**. Has a very developer-friendly package ecosystem. Packages are up-to-date, maintained, and usually allow multiple versions of programming languages like Python to be installed side-by-side. Almost everything works out-of-the-box without me having to think about it.

### Shell

I spend a lot of time working in a terminal, so it's important to me that it's nice to use. Several of the tools here simply make it easier to do something I could otherwise do by typing out a longer command.

- **[Atuin](https://atuin.sh/)**. Store shell history in a sqlite database. I don't use all of it's features, but the interactive UI helps me find commands from my shell history much faster.
- **[Direnv](https://direnv.net/)**. Load `.envrc` and `.env` files in the current directory. This makes it really easy to manage environment variables for various projects, without making a mess of my global shell.
- **[Starship](https://starship.rs/)**. Shell prompt system. Keeps important information front-and-center when working in a terminal. I almost exactly replicated my previous zsh configuration, which was hand-built over years. Works in any shell, so I'm not as tied to zsh as I once was.
- **[zoxide](https://github.com/ajeetdsouza/zoxide)**. Quickly jump to recent directories. It saves a lot of time not needing to type out full paths or remember where things are when working in a terminal.
- **[ack](https://beyondgrep.com/)**. Quickly search codebases. Defaults to recursive search and ignoring directories like `.git` or `node_modules`, making it a lot easier to use than `grep`.
- **[bat](https://github.com/sharkdp/bat)** and **[exa](https://the.exa.website/)**. A `cat` replacement with syntax highlighting, and a `ls` replacement with slightly nicer output.
- **[gh](https://github.com/cli/cli)**. Automate some common GitHub tasks. I mostly use this to clone repositories quickly. I use [GitHub Desktop](https://desktop.github.com/) instead when I need to work with git repositories on Windows machines.

### Configuration management

I generally prefer to have all the tools I need installed on my local development machine. I tend to avoid using Docker or Podman for local development, which helps avoid conflicts when using someone else's workflow that does.

- **[Ansible](https://github.com/ansible/ansible)**. I use Ansible to manage my development machines. It's a lot more flexible than other approaches I've used or seen for managing dotfiles. It's a nice way to abstract over all the different types of packages I need to install.
- **[Poetry](https://github.com/python-poetry/poetry/)**. Manage Python dependencies. There's lots of options in this space, but Poetry works well for me.
- **[pipx](https://pypa.github.io/pipx/)**. Install Python executables in a dedicated space. Keeps the Python tools I use separate from my system installation of Python and separate from codebase-specific virtualenvs.
- **[npx](https://www.npmjs.com/package/npx)**. Run NodeJS exectuables without installing them.

### Cloud systems

These are tools that mostly make a different tool easier to use.

- **[aws-vault](https://github.com/99designs/aws-vault/)**. Manage AWS credentials. Integrates with your system keyring and issues temporary credentials when needed. Makes it a lot easier to manage lots of different AWS roles.
- **[kubectx + kubens](https://github.com/ahmetb/kubectx)**. Quickly switch between Kubernetes contexts and namespaces. I don't know why this isn't built into the kubectl CLI.
- **[stern](https://github.com/stern/stern)**. Follow logs from multiple containers. If nothing else, not having to restart a `kubectl logs` command every time a deployment or pod restarts is very helpful, but stern also provides a nice interactive interface for reading logs.
