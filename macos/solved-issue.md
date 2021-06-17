# Solved Issue

When I was using Macbook Pro (Mojave) at work or on my own laptop, many problems came and required me to solve them. Unfortunately, the problem does not come only once but often many times.

Whether it's my mistake in using a command or indeed from the other side. For that I will collect all the problems that I found along with the solutions to the problems here.

Have fun and good can help as well 😉

## Table Of Contents

1. [zsh: archive folder command](#zsh-archive-folder-comman)
2. [Delete files starting with ._](#delete-files-starting-with-._)

## zsh: archive folder command

```bash
zip -vr archive-name.zip folder-name/ -x ".DS_Store"
```

## Delete files starting with ._

From the parent, recursively:

```bash
find . -type f -name '._*'
```

After checking append -delete to remove the files:

```bash
find . -type f -name '._*' -delete
```
