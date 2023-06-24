
![GitHub](https://img.shields.io/github/license/gmt4/mpvc)
![GitHub Release Date](https://img.shields.io/github/release-date/gmt4/mpvc)
![GitHub release (latest by date)](https://img.shields.io/github/v/release/gmt4/mpvc)
![GitHub top language](https://img.shields.io/github/languages/top/gmt4/mpvc)
![GitHub lines of Code](https://sloc.xyz/github/gmt4/mpvc/?category=code)

# mpvc 🎧

An mpc-like control interface for mpv with a nearly complete compatibility layer for mpc commands in
addition to GNU style arguments.
This forks [lwillets/mpvc](https://github.com/lwilletts/mpvc) providing some extra goodies such as: improved CLI, TUI, FZF & playing media from YouTube & streaming services.
Check the [Wiki](https://github.com/gmt4/mpvc/wiki) & [Casts](https://gmt4.github.io/mpvc/casts/) for a detailed view of the extra features of this fork.

## QuickInstall ▶️

[mpvc-installer](https://github.com/gmt4/mpvc/blob/master/extras/mpvc-installer) fetch-user: installs mpvc under BINDIR=~/bin/

`curl -fsSL -o mpvc-installer https://github.com/gmt4/mpvc/raw/master/extras/mpvc-installer && sh ./mpvc-installer fetch-user`

## QuickStart

<pre>
 <b># fetch a local copy of the github repo</b>
 git clone https://github.com/gmt4/mpvc/
 <b># use extras/mpvc-installer: just copy/link to your $HOME/bin</b>
 mpvc/extras/mpvc-installer link-user

 <b># use mpvc-fzf to search and play youtube media</b>
 mpvc-fzf -p kupla mirage
 <b># use mpvc to add/load/save media files or online YT URLs</b>
 mpvc add /path/to/your/*.mp3 # or your URLs
 find . -type f -name | mpvc load
 mpvc save my-playlist

 <b># use mpvc-fzf to manage the playlist</b>
 mpvc-fzf -f
 <b># use mpvc-tui to start the tui + desktop notifications</b>
 mpvc-tui -T
</pre>

## Screenshots

mpvc-tui -T: running the mpvc TUI

![mpvc-tui -T screenshot](https://github.com/gmt4/mpvc/blob/master/docs/assets/mpvc-tui.png)

mpvc-fzf -f: running with fzf to manage the playlist

![mpvc-fzf screenshot](https://github.com/gmt4/mpvc/blob/master/docs/assets/mpvc-tui-arch.png)

mpvc-tui -n: running with mpvc-fzf and desktop notifications on the upper-right corner

![mpvc tui+fzf+notifications screenshot](https://github.com/gmt4/mpvc/blob/master/docs/assets/mpvc-tui-fzf.png)

## Dependencies

Required:

- `mpv`
- `socat`: is recommended due to the differing implementations of `netcat` across UNIXes.
- `awk`: a sane version of `awk` is recommended

Recommended extras:

- `curl`
- `fzf`
- `notify-send`

## Install

To install mpvc:

- curl based install: as in in [QuickInstall](#quickinstall-%EF%B8%8F).
- git based install: as in [QuickStart](#quickstart).

## Usage

mpvc requires the use of mpv and its `--input-ipc-server` option.

mpvc automatically opens an ipc-server for you when adding files to be played,
but by default will close the ipc-server when all files have finished playing.

To keep the ipc-server open permanently, use:
```
$ mpv --input-ipc-server=/tmp/mpvsocket
```

You can also specify the default ipc server in your `$XDG_CONFIG_HOME/mpv.conf`
which will make the most recent mpv instance you start be controllable via mpvc:
```
input-ipc-server=/tmp/mpvsocket
```

However, this may not be suitable if you have background music added
to the socket and then open a video using mpv. The new mpv instance will be
controllable through the socket, but the previous instance is not. You can get around
this by adding the video via mpvc, and manually switching to the video.

## Useful Tricks

Some basic tricks are provided in [QuickStart](#quickstart). For more tips on loading/saving/maniputaling the mpv playlist/state, managing av/vf filters, etc. are provided in the [LogBook](https://gmt4.github.io/mpvc/logbook.html).

- Hotkey daemons like [sxhkd](https://github.com/baskerville/sxhkd) can be used
  to bind mpvc commands to key combinations. Alternatively check your window
  manager documentation on how to bind keys to commands.
- Any URL that can be played using mpv can be added to the playlist, e.g. using
  [mps-youtube](https://github.com/mps-youtube/mps-youtube) with `player` set to
  mpvc and `playerargs` set to add.
- mpvc executes faster ~4x faster when using dash symlinked to /bin/sh instead
of bash. Another faster alternative is mksh.
- mpvc should be fully POSIX compliant, meaning it should run on any UNIX-like
variant. Please report an issue if you experience trouble.

## Limitations

Like any piece of software, mpvc is not perfect:

- mpvc does not resolve individual files in a directory unless it is
  currently in or has been inside that directory, giving misleading results about
  the total number of files in the current playlist. This is a limitation of mpv.
- mpvc depends on shell tools. If your shell is misconfigured or you are using
  unusual variants of basic UNIX tools, mpvc is not guaranteed to work. However,
  all effort has been made to make mpvc as POSIX compliant as possible.

Check out the Issue Tracker for further improvements to be made.
