# Productivity

This is a record of my own personal optimizations for productivity.
Each one of these optimizations is something I've found has a huge payoff.

For motivation, see [this XKCD](https://xkcd.com/1205/).

## Choice of OS
I prefer to use Mac rather than Linux as my primary development platform.
I can just hear the critics ... and I realize this is a big choice.  But for me,
it comes down to being able to tweak various things that make a big difference to me.
While Ubuntu, GNOME, etc. allow for a lot of tweakability, my personal experience has been:
* the first-class support for these customizations is lacking - especially non-standard keybindings
* I end up spending all the time I would save from optimizations debugging various things that
ya just gotta debug when you use Linux.  And then some.

The hardcore Linux folks will say the points above are not true, or less/no longer true these days.
That may be, but it's a relatively large and uncertain investment for me to determine whether
that's true *for me, and my use cases*.

In any case, many of these optimizations aren't just for Mac, or have decent equivalents on Linux.

For Windows users, of course, I assume that you're already SOL and cannot be saved.

## Using the keyboard
I find that in almost every case, using the keyboard is better than using the mouse.
There are exceptions, but for me, they are rare.

### Vimium for browsing Chrome with the keyboard
I never click on links in web pages if I don't have to.
Instead, I use [Vimium on Chrome](https://chrome.google.com/webstore/detail/vimium/dbepggeogbaibhgnhhndojpepiihcmeb?hl=en).

### Karabiner elements for home row key bindings everywhere
On Mac (see above), I definitely use [Karabiner Elements](https://karabiner-elements.pqrs.org/)
to support first-class home row computing. That is ...

* I never move my hands from the primary "home row" position unless I have to.
In particular, I avoid horizontal motion (e.g. pick up hand, move to arrow keys, put down hand)
because it is much less efficient
* For arrow keys, I have custom Karabiner key bindings that allow me to use VIM-style `ijkl`.
* I never hit the ESC key unless I have to; I bind CapsLock to it, since let's face it, when was
the last time you wanted to use that key for caps lock?  (Sadly, this doesn't work in PyCharm.)
* I have Karabiner bindings for forward/backward word functionality in *all* applications.


### Spectacle for resizing and moving windows
I never manually use the mouse to reposition/resize windows.  Ever.  I use [Spectacle](https://www.spectacleapp.com/).
And of course, I've customized the key bindings so I can do everything from the home row.

### Contexts for switching applications and windows
I use [Context](https://contexts.co/) to switch applications.  This is much, much more powerful
than the default OSX switcher.  You can alt-tab individual instances of applications (e.g. multiple
Chrome windows) in the same interface as different applications.  

## homeslice pattern to keep track of home directory files
I keep all my useful config files in a private git repo using what I call the "homeslice" pattern.
This is where your home directory is itself the root of a git repo.  The key trick is to only
commit the files you want, rather than the many files under your home directory.  The way to do this is:

1. `git init` in your home directory
2. `echo '*' > .gitignore`
3. `git add -f .gitignore`
4. `git commit -m "first commit"`

This creates a git repo with **everything* ignored by default.  Then, to add e.g. `.bashrc`
(which I highly recommend), you just `git add -f .bashrc`.  

It's slightly more subtle to clone into your home on a second machine.  You can e.g.

1. ssh to the second machine, and cd to your home directory
2. `git clone <cloneable path to your homeslice repo> tmp_homeslice`
3. `mv tmp_homeslice/.git .`
4. `rm -rf tmp_homeslice`

as a start.  But **from this point** be careful because doing something like `git checkout .`
is either going to be one of these things:
* just fine, because none of the tracked files in your homeslice is different on the second machine,
and/or you don't mind losing those
* terrible because the second machine had interesting differences that you want to save

In the second case, I'm not going to make recommendations, since the solutions depend on context,
and if you're good enough at git that you're using homeslice, you should probably be able to
figure it out.

To avoid any difficulties, it's best to start with homeslice everywhere before things diverge.
