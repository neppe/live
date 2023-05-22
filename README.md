<p align="center">
    <a> <img src=.assets/logo.png></a>
    <br />
    <br />
	<a href="https://github.com/neppe/pippi-tv/stargazers"><img src="https://img.shields.io/github/stars/neppe/pippi-tv?color=orange&logo=github&style=flat-square"></a>
	<a href="https://github.com/neppe/pippi-tv/graphs/contributors"><img src="https://img.shields.io/github/contributors/neppe/pippi-tv?style=flat-square"></a>
	<img src="https://img.shields.io/static/v1?color=%231831ad&message=Euro20179&label=Maintainer&style=flat-square" alt="Maintainer: Euro20179">
	<a href="https://github.com/neppe/pippi-tv/releases/tag/v1.1.1"><img src="https://img.shields.io/github/v/tag/neppe/pippi-tv?style=flat-square"> </a>
	<a href="https://github.com/neppe/pippi-tv/commits/master"><img src="https://img.shields.io/github/commit-activity/m/neppe/pippi-tv?color=green&style=flat-square"></a>
	<a href="https://discord.gg/kupWznHjRJ"><img src="https://img.shields.io/discord/815609275644117022?color=yellow&logo=discord&style=flat-square" alt="Discord"></a>
	<a href="https://matrix.to/#/#pippi-tv-chat:matrix.org"><img src="https://img.shields.io/static/v1?color=%230eb687&message=chat&logo=matrix&label=matrix&style=flat-square" alt="Discord"></a>
    <br />
    <br />
    <i>A POSIX script that helps you find Youtube videos (without API) and opens/downloads them using mpv/youtube-dl</i>
	<hr>
</p>

<h1 align="center">
	This is a little showcase
</h1>
<p align="center">
<img src=.assets/pippi-tv.gif width="100%">
</p>

---

# Table Of Contents

* [`Dependencies`](#Dependencies)
* [`Install`](#Install)
* [`Features`](#Features)
* [`Examples`](#Examples)
* [`Configuration`](#Configuration)
* [`Bugs`](#Bugs)
* [`Contributing`](#Contributing)
* [`Credits`](#Credits)

---

# Dependencies

There are only 2 required dependencies, however the rest require some configuration before you can replace them.

## Requried dependencies

* [`jq`](https://github.com/stedolan/jq)
* [`curl`](https://github.com/curl/curl)

## Recommended dependencies

* [`mpv`](https://github.com/mpv-player/mpv) (the default video and audio player)
* [`fzf`](https://github.com/junegunn/fzf) (the default menu selection screen)

## Optional dependencies

* [`yt-dlp`](https://github.com/yt-dlp/yt-dlp) (for downloading)
* [`dmenu`](https://tools.suckless.org/dmenu/) (only if using the -D option)
* [`ueberzugpp`](https://github.com/jstkdng/ueberzugpp)
    * needed for the following thumbnail viewers:
        * `kitty`, `iterm2`, `sixel`, and `ueberzug`
    * the original [`ueberzug`](https://github.com/seebye/ueberzug) or any fork may be used if you only want to use the `ueberzug` viewer.

### Thumbnail Viewers

* **To use a thumbnail viewer include `-T <viewer>` in the command when running pippi-tv**

| Program                                                                   | Wayland Support      |
| :--                                                                       | :--                  |
| [`kitty`](https://github.com/kovidgoyal/kitty) (requires `ueberzugpp`)    | &#9989;              |
| `iterm2` (requires `ueberzugpp`)                                          | &#9989;              |
| `sixel` (requires `ueberzugpp`)                                           | &#9989;              |
| [`chafa`](https://github.com/hpjansson/chafa)                             | &#9989;              |
| [`catimg`](https://github.com/posva/catimg)                               | &#9989;              |
| [`imv`](https://git.sr.ht/~exec64/imv)                                    | &#9989;              |
| [`mpv`](https://github.com/mpv-player/mpv)                                | &#9989;              |
| [`swayimg`](https://github.com/artemsen/swayimg)                          | only on `sway`       |
| [`swayimg`](https://github.com/artemsen/swayimg) (-T swayimg-hyprland)    | only on `hyprland`   |

# Install

<a href="https://repology.org/metapackage/pippi-tv">
    <img src="https://repology.org/badge/vertical-allrepos/pippi-tv.svg" alt="Repo status" align="right">
</a>

**if on `linux` and installed using make on version `2.0` or prior, run `sudo make uninstall-old` first**

1. Install the dependencies listed [above](#Dependencies)
2. Run the following commands
```sh
git clone https://github.com/neppe/pippi-tv
cd pippi-tv
sudo make install doc
```

* If you wish to not install documentation (highly unrecommended) run `sudo make install` instead.

* If you wish to install addons, run `sudo make addons`
    * `YTFZF_SYSTEM_ADDONS_DIR` will point to `/usr/local/share/pippi-tv/addons` even if you set `PREFIX` to something else
    * If you use a different prefix, it would be smart to export `YTFZF_SYSTEM_ADDONS_DIR` to `$PREFIX/share/pippi-tv/addons` in a shell startup file.

* You may also install `pippi-tv` through your package manager, as listed on the side.

## Addons

Addons are extra features that will not be as supported as everything built into `pippi-tv` itself.

Addons are located in `addons`, copy any addon to `~/.config/pippi-tv/{addon-type}/{addon}`, and give it execute permissions.

You may also just copy the entire addon folder type, eg: `cp -r addons/thumbnail-viewers ~/.config/pippi-tv/`

### Usage

To use a scraper addon run `pippi-tv -c <scraper> ...`

To use a thumbnail-viewer addon run `pippi-tv -T <viewer> ...`

To use a interface addon run `pippi-tv -i <interface> ...`

To use a url-handler addon run `pippi-tv -u <handler> ...`

To use a sort-name addon run `pippi-tv --sort-name=<sort-name> ...`

To use an extension addon run `pippi-tv -e <extension> ...`

---

# Features

* Subscriptions
* Thumbnails
* Watch history
* Search History
* Downloading
* Queueing multiple videos
* Custom menus, and scrapers
* Addon support

---

# Examples

> Search with thumbnails

```sh
pippi-tv -t <search>
```

> Use `dmenu` as the menu instead of `fzf`

```sh
pippi-tv -D <search>
```

> Print the link of the selected video instead of playing it

```sh
pippi-tv -L <search>
```

> Search Odysee instead of youtube

```sh
pippi-tv -cO <search>
```

> Use the chafa thumbnail viewer, pass --vo=sixel, and --quiet to mpv, scrape odysee with the search *odysee search*, youtube with the search: *youtube search*, and also scrape subscriptions

```sh
pippi-tv -t -T chafa --url-handler-opts='--vo=sixel --quiet' -cO,Y,SI --multi-search odysee search,youtube search
```

---

# Configuration

Everything that is an option can also be configured in `~/.config/pippi-tv/conf.sh`.

In addition, the video player and other things may be changed here

Here is a [sample configuration](docs/conf.sh) (please dont use it)

For more information, see `pippi-tv(5)` which should be installed, if it's not see [the wiki](https://github.com/neppe/pippi-tv/wiki).

---

# Bugs

* *dwm with swallow patch: Images don't render with ueberzug when looped (ie, option `-l`)*
* *if thumbnails are not working `.Xauthority` might be causing it. Try deleting it and relogging into your computer.*

# Contributing

Feel free to contribute, and add your name to the credits, please use the development branch. For more information see [contributing](CONTRIBUTING.md)

# Credits

| User           | Contributions                             | Donate|
| :---           | :---                                      | :--- |
| neppe    | [contributions](credits/neppe.md)    ||
| Euro20179     | [contributions](credits/euro20179.md)     ||
| Simonhughxyz  | [contributions](credits/simonhughxyz.md)  ||
| Jac-Zac       | [contributions](credits/jac-zac.md)       ||
| Mudskipper875 | [contributions](credits/mudskipper875.md) ||
| Gardockt | [contributions](credits/gardockt.md)||
| qoheniac | [contributions](credits/qoheniac.md)||
| mathisto | [contributions](credits/mathisto.md)||

