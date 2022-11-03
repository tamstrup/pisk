# pisk

The simplest way imaginable for talking to a Postgres session from Vim.

<a href="https://asciinema.org/a/534589" target="_blank"
style="text-decoration: none">
<img src="https://github.com/patrkris/pisk/blob/master/demo.gif">
</a>

## Requirements

Bash, psql, and a working installation of netcat.

## Installation

Just put the `pisk` executable bash script somewhere in your _PATH_.

## How

The script `pisk` starts a netcat server and pipes its output to psql.
To send a command to psql it's just a matter of using a netcat client,
i.e.,
```bash
$ nc localhost 3000
select 1;
```
and hit _Enter_.

To make this work in Vim, I suggest these two mappings in .vimrc (on
macOS):

```viml
augroup mine
  autocmd FileType sql nn <leader><Enter>
        \ vap:term ++close ++hidden nc localhost 3000<CR>
  autocmd FileType sql vn <leader><Enter>
        \ :term ++close ++hidden nc localhost 3000<CR>
augroup END
```

The first mapping will send the current paragraph to psql. The second
will send the visual selection to psql.

To start `pisk`, use the Vim command `:term pisk`.

## Why

It was already easy to execute text from Vim with psql by either using
the `!` command or via `:term`. I often wanted to maintain a psql session
for a longer period of time that I could send commands to, or start a
transaction with. Pisk allows you to do this.

## Improvements

There are many ways to improve pisk and the Vim integration mentioned
above. For instance, there is currently no way of saying "execute this
complete statement" like you do by default in tools like Postico or
TablePlus. With the above Vim mappings you either say "pipe this
paragraph to psql" or "pipe this visual selection to psql".

<!-- vim: set tw=72: -->
