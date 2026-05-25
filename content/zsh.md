---
publish: true
created: 2026-01-29T21:35:22.000+01:00
modified: 2026-04-11T14:40:02.211+02:00
tags:
  - Tech/OS/Linux
---

It’s a **terminal framework** that lets you create custom configurations for your terminal through the `~/.zshrc` file. You can edit it with: `code ~/.zshrc`

## MacOS 10.15 Catalina and Above

Apple [switched](https://web.archive.org/web/20190826201542/https://www.theverge.com/2019/6/4/18651872/apple-macos-catalina-zsh-bash-shell-replacement-features) their default shell to **zsh**, so the config files include `~/.zshenv` and `~/.zshrc`. This is just like `~/.bashrc`, but for zsh. Just edit the file and add what you need; it should be sourced every time you open a new terminal window:

`nano ~/.zshenv` `alias py=python`

Then do ctrl+x, y, then enter to save.

This file seems to be executed no matter what (login, non-login, or script), so seems better than the `~/.zshrc` file.

- [How do I create a Bash alias?](https://stackoverflow.com/questions/8967843/how-do-i-create-a-bash-alias)
- [I can't find my alias file](https://askubuntu.com/questions/1386031/i-cant-find-my-alias-file)

---

## Examples

### iA Writer

open `nano ~/.zshenv` and add `ia="open $1 -a /Applications/iA\ Writer.app"` to open MD files with `ia filename.md`

OR `alias -g ia="open $1 -a /Applications/iA\ Writer.app"`

[open iA writer from the command line](https://gist.github.com/brendanjerwin/996464)
[Alternative](https://gist.github.com/brendanjerwin/996464)
