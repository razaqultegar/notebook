# Solved Issue

When I was using Linux (Ubuntu 18.04) at work or on my own laptop, many problems came and required me to solve them. Unfortunately, the problem does not come only once but often many times.

Whether it's my mistake in using a command or indeed from the other side. For that I will collect all the problems that I found along with the solutions to the problems here.

Have fun and good can help as well 😉

## Table Of Contents

1. [zsh: laravel command not found](#zsh-laravel-command-not-found)

2. [XAMPP:  Another web server is already running.](#xampp-another-web-server-is-already-running)

## zsh: laravel command not found

```bash
sudo nano ~/.zshrc
# and add the following script:
alias laravel="~/.config/composer/vendor/bin/laravel"
# or
alias laravel="~/.composer/vendor/bin/laravel"
```

## XAMPP: Another web server is already running.

```bash
sudo netstat -nap | grep :80
# see, which port is currently using apache2
# for this case i will use: 1035/apache2
# and i will stop it
sudo kill 1035
# start again
sudo /opt/lampp/lampp start
```
