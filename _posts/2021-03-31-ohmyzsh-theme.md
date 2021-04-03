---
title: "Oh My ZSH - Setup Terminal for Ubuntu 20.04"
category: articles
tags:
 - misc
---

Here is my current terminal setup for Ubuntu 20.04. 
![theme](/assets/images/theme-screenshot-2021-04-03.png)

I have used [Ohmyzsh](https://ohmyz.sh/#install) to get this done. To install oh-my-zsh please follow the instructions on their homepage.

```sh
$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

I then installed the awesome [PowerLevel10](https://github.com/romkatv/powerlevel10k#oh-my-zsh) theme for omz using this step:

```sh
$ git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

Here is the note from P10K's readme about configuration -

> On the first run, Powerlevel10k configuration wizard will ask you a few questions and configure your prompt. If it doesn't trigger automatically, type p10k configure. Configuration wizard creates ~/.p10k.zsh based on your preferences. Additional prompt customization can be done by editing this file. It has plenty of comments to help you navigate through configuration options.