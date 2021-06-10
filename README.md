# vimdict

a shell script for reading definition of words and phrases,
and looking up dictionaries, using [dict](https://wiki.archlinux.org/title/Dictd).

it requires dict and vim (or nvim, or any other vim-compatible editor).

## install vimdict

archlinux users can use the **AUR package** (vimdict-git)[https://aur.archlinux.org/packages/opener-git]:

```
$ paru -S vimdict-git
```

otherwise:

```
$ git clone https://github.com/soystemd/vimdict
$ cd vimdict
$ sudo make install
```

while viewing definitions in vim, you can press **shift+k** on any word
to look up the definition of that word in a new vim buffer
(making use of vim's keyword lookup feature).

see `vimdict -h` for more info.

## install dict

1. install `dictd` from your distro's package manager.
2. add `server dict.org` at the top of `/etc/dict/dict.conf`.

now you can get word/phrase definitions by running:

```
$ dict <word-or-phrase>
```

provided you have an internet connection.

## offline dictionaries

with the above config, dict gets definitions from dict.org,
which of course requires an internet connection.
but if you want to have offline dictionaries:

1. install `dict-gcide` and `dict-wn` (or any dictionary package you like).
2. add your dictionaries to `/etc/dict/dictd.conf`.

example entry for dict-gcide:

```
database gcide {
	data /usr/share/dictd/gcide.dict.dz
	index /usr/share/dictd/gcide.index
}
```

3. start dictd:

```
$ sudo systemctl start dictd.service
```

4. add `server localhost` at the top of `/etc/dict/dict.conf`.

now dict will get definitions from the locally running dictd server.
