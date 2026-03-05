# Firefox Auto Hide Tab Bar

By Morgan Aldridge <morgant@makkintosshu.com>

## OVERVIEW

A common annoyance with modern web browsers when run in desktop environments
and window managers which provide window decorations (e.g. title bar and
min/max/close buttons), especially [Firefox](https://www.firefox.com/), is
that the tab bar is always visible, even when it contains only a single tab.
This wastes vertical screen real estate, especially because the current
(read: only) tab title is redundant to that of the window's title bar.

This Firefox `userChrome.css` customization resolves this by restoring a
once-common feature of "tabbed browsing": automatically showing/hiding the
entire tab bar (including buttons) based on the number of tabs.
Specificially, it:

* Automatically hides the tab bar when it contains only one tab, including:
    * The tab, itself
    * The "new tab" button ('+')
    * The "all tabs" button/menu ('&or;')
    * 'Private' mode indicator
    * Moves window controls (min/max/close buttons) into the toolbar if  
        Firefox windows are using [client-side decorations  
        (CSD)](https://en.wikipedia.org/wiki/Client-side_decoration)
* Automatically shows the tab bar when it contains multiple tabs

**Note:** When the tab bar is hidden, one can still open a new tab from the
Firefox main menu or via keyboard shortcuts.

**IMPORTANT:** _Unfortunately, this is not possible to implement as an
extension in Firefox, only via `userChrome.css` customization. This requires
special Firefox configuration and local installation of files. See detailed
installation instructions below._

## COMPATIBILITY

This `userChrome.css` has been tested and confirmed to work in Firefox
versions 128.3.0 through 147.0.4 under [OpenBSD](https://www.openbsd.org)
and [macOS](https://www.apple.com/os/macos/). It has only been tested as **the
only** `userChrome.css` installed.

It is intended to be used with the following Firefox configuration:

* "Title Bar" turned on
* "Vertical Tabs" turned off

While I strive for compatibility with other `userChrome.css` customizations,
due to the nature of CSS and the high likelihood and long history of Firefox
introducing breaking-changes with new versions, I cannot guarantee it will
work for you. Especially when combined with other `userChrome.css`
customizations.

If it's not working or causing UI/UX issues, please do not use it.

## IMPLEMENTATION

This is based on an example provided in [this comment on an r/firefox (Reddit)
post](https://www.reddit.com/r/firefox/comments/1h3l8sf/comment/m00a26w/),
plus a trick to preserve window controls from [this comment on an
irvinm/Toggle-Native-Tab-Bar GitHub issue](https://github.com/irvinm/Toggle-Native-Tab-Bar/issues/3#issuecomment-2556331029).
It is implemented as a separate `auto-hide-tab-bar.css` file which can be
imported into your `userChrome.css` for easier and safer integration with
other customizations.

**NOTE:** This _does not_ re-style/relocate the tab title to show it
elsewhere in the Firefox window, unlike some alternatives linked below.
This is because I run a window manager which provides a full title bar with
window controls ([MLVWM](https://github.com/morgant/mlvwm), specifically), so
the title is already displayed (therefore redundant.) I also disable
[client-side decorations (CSD)](https://en.wikipedia.org/wiki/Client-side_decoration),
but have implemented moving window controls in case CSD gets re-enabled or for
use it under another OS, desktop environment(DE), and/or window manager (WM).

## INSTALLATION

1. In Firefox:
    1. Enable `userChrome.css` support:
        1. Type `about:config` in the address/search bar and press return
        2. Set the `toolkit.legacyUserProfileCustomizations.stylesheets`  
            setting to `true`
        3. Optional, but _highly encouraged_: Set the `browser.tabs.inTitlebar`  
            setting to `0` (zero; default: `2`)
    2. Locate your Firefox profile directory:
        1. Type `about:profiles` in the address/search bar and press return
        2. Look for the profile with "This is the profile in use and it cannot  
            be deleted"
        3. Note the "Root Directory" path for use in the next step (**NOT**  
            the "Local Directory")
2. Create `chrome/userChrome.css` in your local profile directory:
    1. On your computer (in a file browser or a terminal), navigate to the  
        profile's "Root Directory", as noted above (e.g.  
        `cd ~/.mozilla/<profile-root-dir>`)
    2. Create a new `chrome` subdirectory and navigate into it (e.g.  
        `mkdir chrome && cd chrome`)
    3. Make a new `userChrome.css` file (e.g. `touch userChrome.css`)
3. Install `chrome/auto-hide-tab-bar.css`:
    1. Copy the `chrome/auto-hide-tab-bar.css` file from this repository into  
        your profile's `chrome` subdirectory
    2. Edit the `userChrome.css` file in your profile's `chrome` subdirectory  
        to add the following line:  
        ```
        @import "./auto-hide-tab-bar.css";
        ```
4. Quit and relaunch Firefox to load your profile's updated  
    `chrome/userChrome.css` files (it is **only** loaded at launch)

## ALTERNATIVES

* [firefox-hide-tabs](https://github.com/geoffreytools/firefox-hide-tabs)
* [Toggle Native Tab Bar](https://github.com/irvinm/Toggle-Native-Tab-Bar)

## A BRIEF HISTORY OF TABBED BROWSING

While I was an early adopter of Firefox, I don't remember the specific feature
sets of the browsers at that time. According to the [history
section](https://en.wikipedia.org/wiki/Tab_(interface)#History) of
[Wikipedia's Tab (interface) article](https://en.wikipedia.org/wiki/Tab_(interface))
and the [Wayback Machine's 2004-11-10 archive of the "Mozilla Firefox - Tabbed
Browsing" page](https://web.archive.org/web/20041110012651/http://www.mozilla.org/products/firefox/tabbed-browsing.html), Firefox appears to be one of the earlier browsers to implement "tabbed
browsing". Most notably, while other browsers (including Opera and Mozilla's
own "Mozilla") supported tabbed browsing, Firefox was the first to have 
widespread adoption (see the [History: Versions](https://en.wikipedia.org/wiki/Firefox#Versions)
section of [Wikipedia's Firefox article](https://en.wikipedia.org/wiki/Firefox)
for further details.

## LICENSE

Released under the [MIT License](LICENSE).
